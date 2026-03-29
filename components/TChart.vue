<script setup>
defineProps({
  leftTitle: { type: String, default: 'Current State' },
  rightTitle: { type: String, default: 'Future State' },
  leftColor: { type: String, default: '#ef4444' },
  rightColor: { type: String, default: '#16a34a' },
  leftItems: {
    type: Array,
    required: true
  },
  rightItems: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <div class="t-chart">
    <!-- Header row -->
    <div class="column-title" :style="{ color: leftColor }">{{ leftTitle }}</div>
    <div class="divider-header"></div>
    <div class="column-title" :style="{ color: rightColor }">{{ rightTitle }}</div>

    <!-- Paired rows -->
    <template v-for="(item, idx) in leftItems" :key="idx">
      <div
        class="item left-item"
        :style="{ borderLeftColor: `${leftColor}60` }"
      >
        {{ item.text }}
      </div>
      <div class="divider-cell">
        <span>→</span>
      </div>
      <div
        class="item right-item"
        :style="{ borderLeftColor: rightColor }"
      >
        <span class="item-text">{{ rightItems[idx]?.text }}</span>
        <span v-if="rightItems[idx]?.highlight" class="item-highlight" :style="{ color: rightColor }">{{ rightItems[idx].highlight }}</span>
      </div>
    </template>
  </div>
</template>

<style scoped>
.t-chart {
  display: grid;
  grid-template-columns: 1fr 24px 1fr;
  gap: 0;
  margin-top: 1rem;
  align-items: stretch;
}

.column-title {
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.divider-header {
  margin-bottom: 0.5rem;
}

.item {
  padding: 0.5rem 0.8rem;
  border-left: 3px solid;
  margin-bottom: 0.4rem;
  font-size: 0.75rem;
  display: flex;
  align-items: center;
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
  font-size: 0.7rem;
}

.divider-cell {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
  color: #ccc;
  margin-bottom: 0.4rem;
}
</style>
