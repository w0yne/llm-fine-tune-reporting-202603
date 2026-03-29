<script setup>
defineProps({
  leftTitle: { type: String, default: 'Current State' },
  rightTitle: { type: String, default: 'Future State' },
  leftColor: { type: String, default: '#ef4444' },
  rightColor: { type: String, default: '#16a34a' },
  leftItems: {
    type: Array,
    required: true
    // Each: { text: string }
  },
  rightItems: {
    type: Array,
    required: true
    // Each: { text: string, highlight?: string }
  }
})
</script>

<template>
  <div class="t-chart">
    <div class="left-column">
      <div class="column-title" :style="{ color: leftColor }">{{ leftTitle }}</div>
      <div
        v-for="(item, idx) in leftItems"
        :key="idx"
        class="item left-item"
        :style="{ borderLeftColor: `${leftColor}60` }"
      >
        {{ item.text }}
      </div>
    </div>

    <div class="divider">
      <span>→</span>
    </div>

    <div class="right-column">
      <div class="column-title" :style="{ color: rightColor }">{{ rightTitle }}</div>
      <div
        v-for="(item, idx) in rightItems"
        :key="idx"
        class="item right-item"
        :style="{ borderLeftColor: rightColor }"
      >
        <span class="item-text">{{ item.text }}</span>
        <span v-if="item.highlight" class="item-highlight" :style="{ color: rightColor }">{{ item.highlight }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.t-chart {
  display: grid;
  grid-template-columns: 1fr 30px 1fr;
  gap: 0;
  margin-top: 1.5rem;
  align-items: start;
}

.left-column,
.right-column {
  display: flex;
  flex-direction: column;
}

.column-title {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-bottom: 0.8rem;
  font-weight: 600;
}

.item {
  padding: 0.7rem 1rem;
  border-left: 3px solid;
  margin-bottom: 0.5rem;
  font-size: 0.8rem;
}

.left-item {
  background: #fef2f2;
  color: #991b1b;
}

.right-item {
  background: #f0fdf4;
  font-weight: 500;
}

.item-highlight {
  margin-left: 0.3rem;
  font-size: 0.75rem;
}

.divider {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  font-size: 1.5rem;
  color: #ccc;
}
</style>
