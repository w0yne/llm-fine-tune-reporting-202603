<script setup>
defineProps({
  stats: {
    type: Array,
    required: true
    // Each: { value: string, label: string, color?: string }
  }
})
</script>

<template>
  <div class="stat-highlight">
    <div
      v-for="(stat, idx) in stats"
      :key="idx"
      class="stat"
    >
      <div class="stat-value" :style="{ color: stat.color || '#0284c7' }">{{ stat.value }}</div>
      <div class="stat-label">{{ stat.label }}</div>
    </div>
  </div>
</template>

<style scoped>
.stat-highlight {
  display: flex;
  justify-content: center;
  gap: 3rem;
}

.stat {
  text-align: center;
}

.stat-value {
  font-size: 2rem;
  font-weight: 700;
}

.stat-label {
  font-size: 0.75rem;
  color: #888;
}
</style>
