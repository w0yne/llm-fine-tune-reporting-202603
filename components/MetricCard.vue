<script setup>
defineProps({
  status: { type: String, default: 'green' }, // 'green' | 'yellow' | 'red'
  icon: { type: String, default: '✓' },
  title: { type: String, required: true },
  value: { type: String, required: true },
  target: { type: String, default: '' },
  delta: { type: String, default: '' }
})

const statusColors = {
  green: '#16a34a',
  yellow: '#d97706',
  red: '#ef4444'
}

const statusIcons = {
  green: '✓',
  yellow: '!',
  red: '✕'
}
</script>

<template>
  <div class="metric-card">
    <div class="status-indicator" :style="{ backgroundColor: statusColors[status] }">
      <span>{{ statusIcons[status] }}</span>
    </div>
    <div class="metric-title">{{ title }}</div>
    <div class="metric-value" :style="{ color: statusColors[status] }">{{ value }}</div>
    <div v-if="target" class="metric-target">Target: {{ target }}</div>
    <div v-if="delta" class="metric-delta" :style="{ color: statusColors[status] }">{{ delta }}</div>
  </div>
</template>

<style scoped>
.metric-card {
  padding: 1.2rem;
  border: 1px solid #e5e7eb;
  border-radius: 10px;
  text-align: center;
}

.status-indicator {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  margin: 0 auto 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.status-indicator span {
  color: white;
  font-size: 1.1rem;
}

.metric-title {
  font-size: 0.8rem;
  font-weight: 600;
}

.metric-value {
  font-size: 1.3rem;
  font-weight: 700;
  margin: 0.2rem 0;
}

.metric-target {
  font-size: 0.7rem;
  color: #888;
}

.metric-delta {
  font-size: 0.65rem;
  font-weight: 500;
  margin-top: 0.2rem;
}
</style>
