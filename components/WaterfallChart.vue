<script setup>
const props = defineProps({
  bars: {
    type: Array,
    required: true
    // Each bar: { label: string, sublabel?: string, value: string, height: number, color: string, isTotal?: boolean, offset?: number }
  },
  height: { type: Number, default: 280 },
  barWidth: { type: Number, default: 70 },
  showCallout: { type: Boolean, default: false },
  calloutText: { type: String, default: '' }
})
</script>

<template>
  <div class="waterfall-chart">
    <div class="chart-area" :style="{ height: `${height}px` }">
      <div
        v-for="(bar, idx) in bars"
        :key="idx"
        class="bar-wrapper"
        :style="{ marginBottom: bar.offset ? `${bar.offset}px` : '0' }"
      >
        <div class="bar-value" :style="{ color: bar.isTotal ? '#111' : bar.color }">
          {{ bar.value }}
        </div>
        <div
          class="bar"
          :style="{
            width: `${barWidth}px`,
            height: `${bar.height}px`,
            backgroundColor: bar.color
          }"
        ></div>
        <div class="bar-label">
          {{ bar.label }}<br v-if="bar.sublabel" /><span v-if="bar.sublabel">{{ bar.sublabel }}</span>
        </div>
      </div>
    </div>
    <div v-if="showCallout && calloutText" class="callout">
      <span>{{ calloutText }}</span>
    </div>
  </div>
</template>

<style scoped>
.waterfall-chart {
  width: 100%;
}

.chart-area {
  display: flex;
  align-items: flex-end;
  justify-content: center;
  gap: 0.4rem;
}

.bar-wrapper {
  text-align: center;
}

.bar-value {
  font-size: 0.7rem;
  font-weight: 600;
  margin-bottom: 0.3rem;
}

.bar {
  border-radius: 4px 4px 0 0;
}

.bar-label {
  font-size: 0.65rem;
  color: #888;
  margin-top: 0.3rem;
  line-height: 1.3;
  white-space: nowrap;
}

.callout {
  text-align: center;
  margin-top: 0.5rem;
  padding: 0.5rem;
  background: #f0f9ff;
  border-radius: 6px;
}

.callout span {
  font-size: 0.8rem;
  color: #0284c7;
  font-weight: 500;
}
</style>
