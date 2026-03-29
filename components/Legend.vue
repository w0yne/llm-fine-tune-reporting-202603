<script setup>
defineProps({
  items: {
    type: Array,
    required: true
    // Each: { color: string, label: string }
  },
  layout: { type: String, default: 'horizontal' } // 'horizontal' | 'vertical'
})
</script>

<template>
  <div class="legend" :class="[`layout-${layout}`]">
    <div v-for="(item, idx) in items" :key="idx" class="legend-item">
      <div class="legend-color" :style="{ backgroundColor: item.color }"></div>
      <span>{{ item.label }}</span>
    </div>
  </div>
</template>

<style scoped>
.legend {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

.layout-horizontal {
  gap: 2rem;
  flex-direction: row;
}

.layout-vertical {
  gap: 0.5rem;
  flex-direction: column;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 0.3rem;
}

.legend-color {
  width: 12px;
  height: 12px;
  border-radius: 2px;
}

.legend-item span {
  font-size: 0.7rem;
  color: #888;
}
</style>
