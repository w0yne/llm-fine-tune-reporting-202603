<script setup>
defineProps({
  bars: {
    type: Array,
    required: true
    // Each bar: { label: string, value: string | number, width: number (percentage), color: string, highlight?: boolean }
  },
  maxWidth: { type: Number, default: 650 },
  barHeight: { type: Number, default: 28 },
  labelWidth: { type: Number, default: 90 }
})
</script>

<template>
  <div class="horizontal-bar-chart" :style="{ maxWidth: `${maxWidth}px` }">
    <div v-for="(bar, idx) in bars" :key="idx" class="bar-row">
      <div
        class="bar-label"
        :style="{ width: `${labelWidth}px`, fontWeight: bar.highlight ? 600 : 500, color: bar.highlight ? bar.color : '#333' }"
      >
        {{ bar.label }}
      </div>
      <div class="bar-track" :style="{ height: `${barHeight}px` }">
        <div
          class="bar-fill"
          :style="{
            width: `${bar.width}%`,
            backgroundColor: bar.color,
            height: '100%'
          }"
        >
          <span class="bar-value">{{ bar.value }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.horizontal-bar-chart {
  margin: 0 auto;
}

.bar-row {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 0.8rem;
}

.bar-row:last-child {
  margin-bottom: 0;
}

.bar-label {
  font-size: 0.8rem;
  text-align: right;
}

.bar-track {
  flex: 1;
  background: #f1f5f9;
  border-radius: 4px;
  position: relative;
}

.bar-fill {
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding-right: 0.5rem;
}

.bar-value {
  font-size: 0.7rem;
  color: white;
  font-weight: 600;
}
</style>
