<script setup>
import { computed } from 'vue'

const props = defineProps({
  items: {
    type: Array,
    required: true
    // Each: { label: string, color: string }
  },
  size: { type: Number, default: 350 },
  ringColor: { type: String, default: '#0284c7' },
  centerIcon: { type: String, default: '⟳' }
})

// Compute each item's position along the ring using equal angular spacing
const itemsWithPosition = computed(() => {
  const n = props.items.length
  const radius = (props.size - 50) / 2
  const center = props.size / 2

  return props.items.map((item, i) => {
    // Start from top (-90 deg), go clockwise
    const angle = (i / n) * 2 * Math.PI - Math.PI / 2
    const x = center + radius * Math.cos(angle)
    const y = center + radius * Math.sin(angle)
    return {
      ...item,
      style: {
        left: `${x}px`,
        top: `${y}px`,
        backgroundColor: item.color,
        transform: 'translate(-50%, -50%)'
      }
    }
  })
})
</script>

<template>
  <div class="flywheel">
    <div class="wheel-container" :style="{ width: `${size}px`, height: `${size}px` }">
      <!-- Ring -->
      <div
        class="ring"
        :style="{
          width: `${size - 50}px`,
          height: `${size - 50}px`,
          borderColor: ringColor
        }"
      ></div>

      <!-- Items around the wheel -->
      <div
        v-for="(item, idx) in itemsWithPosition"
        :key="idx"
        class="wheel-item"
        :style="item.style"
      >
        {{ item.label }}
      </div>

      <!-- Center icon -->
      <div class="center-icon" :style="{ color: ringColor }">{{ centerIcon }}</div>
    </div>
  </div>
</template>

<style scoped>
.flywheel {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 320px;
}

.wheel-container {
  position: relative;
}

.ring {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border: 3px solid;
  border-radius: 50%;
}

.wheel-item {
  position: absolute;
  color: white;
  padding: 0.5rem 0.8rem;
  border-radius: 8px;
  font-size: 0.7rem;
  font-weight: 600;
  text-align: center;
  white-space: nowrap;
}

.center-icon {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 1.8rem;
}
</style>
