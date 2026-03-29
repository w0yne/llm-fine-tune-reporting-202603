<script setup>
defineProps({
  groups: {
    type: Array,
    required: true
    // Each group: { label: string, sublabel?: string, bars: [{ value: string, height: number, color: string }] }
  },
  legend: {
    type: Array,
    default: () => []
    // Each: { label: string, color: string }
  },
  highlights: {
    type: Array,
    default: () => []
    // Each: { text: string, color?: string }
  },
  height: { type: Number, default: 250 },
  barWidth: { type: Number, default: 40 }
})
</script>

<template>
  <div class="grouped-bar-chart">
    <div class="chart-area" :style="{ height: `${height}px` }">
      <div v-for="(group, idx) in groups" :key="idx" class="group-wrapper">
        <div class="bars-container">
          <div v-for="(bar, bIdx) in group.bars" :key="bIdx" class="bar-item">
            <div class="bar-value" :style="{ color: bar.color }">{{ bar.value }}</div>
            <div
              class="bar"
              :style="{
                width: `${barWidth}px`,
                height: `${bar.height}px`,
                backgroundColor: bar.color
              }"
            ></div>
          </div>
        </div>
        <div class="group-label">
          {{ group.label }}<br v-if="group.sublabel" /><span v-if="group.sublabel">{{ group.sublabel }}</span>
        </div>
      </div>
    </div>
    <div class="footer">
      <div v-if="legend.length > 0" class="legend">
        <div v-for="(item, idx) in legend" :key="idx" class="legend-item">
          <div class="legend-color" :style="{ backgroundColor: item.color }"></div>
          <span>{{ item.label }}</span>
        </div>
      </div>
      <div v-for="(hl, idx) in highlights" :key="`hl-${idx}`" class="highlight" :style="{ backgroundColor: hl.bgColor || '#f0fdf4' }">
        <span :style="{ color: hl.color || '#16a34a' }">{{ hl.text }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.grouped-bar-chart {
  width: 100%;
}

.chart-area {
  display: flex;
  align-items: flex-end;
  justify-content: center;
  gap: 2rem;
}

.group-wrapper {
  text-align: center;
}

.bars-container {
  display: flex;
  align-items: flex-end;
  gap: 0.3rem;
  justify-content: center;
}

.bar-item {
  text-align: center;
}

.bar-value {
  font-size: 0.6rem;
  font-weight: 600;
  margin-bottom: 0.2rem;
}

.bar {
  border-radius: 4px 4px 0 0;
}

.group-label {
  font-size: 0.75rem;
  color: #888;
  margin-top: 0.3rem;
  line-height: 1.3;
}

.footer {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 1rem;
  align-items: center;
}

.legend {
  display: flex;
  gap: 2rem;
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

.highlight {
  padding: 0.3rem 0.6rem;
  border-radius: 4px;
}

.highlight span {
  font-size: 0.7rem;
  font-weight: 500;
}
</style>
