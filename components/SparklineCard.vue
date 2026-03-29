<script setup>
defineProps({
  title: { type: String, required: true },
  trend: { type: String, default: '' }, // e.g. "↑ 15% YoY"
  trendColor: { type: String, default: '#16a34a' },
  bars: {
    type: Array,
    required: true
    // Each: { height: string (percentage), color: string, highlight?: boolean }
  }
})
</script>

<template>
  <div class="sparkline-card">
    <div class="card-title">{{ title }}</div>
    <div v-if="trend" class="card-trend" :style="{ color: trendColor }">{{ trend }}</div>
    <div class="sparkline">
      <div
        v-for="(bar, idx) in bars"
        :key="idx"
        class="spark-bar"
        :style="{
          height: bar.height,
          backgroundColor: bar.color
        }"
      ></div>
    </div>
  </div>
</template>

<style scoped>
.sparkline-card {
  padding: 1rem;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
}

.card-title {
  font-size: 0.8rem;
  font-weight: 600;
  margin-bottom: 0.3rem;
}

.card-trend {
  font-size: 0.65rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.sparkline {
  display: flex;
  align-items: flex-end;
  gap: 3px;
  height: 60px;
}

.spark-bar {
  flex: 1;
  border-radius: 2px 2px 0 0;
}
</style>
