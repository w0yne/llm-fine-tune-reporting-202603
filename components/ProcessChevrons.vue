<script setup>
defineProps({
  steps: {
    type: Array,
    required: true
    // Each step: { label: string, sublabel?: string, detail?: string, color: string, textColor?: string }
  },
  details: {
    type: Array,
    default: () => []
    // Each: { borderColor: string, items: string[] } - shown below chevrons
  }
})
</script>

<template>
  <div class="process-chevrons">
    <div class="chevrons-container">
      <div
        v-for="(step, idx) in steps"
        :key="idx"
        class="chevron"
        :class="{ first: idx === 0, last: idx === steps.length - 1 }"
        :style="{
          backgroundColor: step.color,
          color: step.textColor || 'white',
          '--chevron-color': step.color
        }"
      >
        <div class="chevron-content">
          <div class="chevron-label">{{ step.label }}</div>
          <div v-if="step.sublabel" class="chevron-sublabel">{{ step.sublabel }}</div>
          <div v-if="step.detail" class="chevron-detail">{{ step.detail }}</div>
        </div>
      </div>
    </div>

    <div v-if="details.length > 0" class="details-grid">
      <div
        v-for="(detail, idx) in details"
        :key="idx"
        class="detail-box"
        :style="{ borderTopColor: detail.borderColor }"
      >
        <div v-for="(item, iIdx) in detail.items" :key="iIdx" class="detail-item">
          {{ item }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.process-chevrons {
  width: 100%;
}

.chevrons-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0;
  margin-top: 2rem;
}

.chevron {
  padding: 1rem 1.5rem 1rem 1.8rem;
  clip-path: polygon(0 0, calc(100% - 15px) 0, 100% 50%, calc(100% - 15px) 100%, 0 100%, 15px 50%);
  min-width: 130px;
  text-align: center;
  margin-left: -1px;
}

.chevron.first {
  padding-left: 1.2rem;
  clip-path: polygon(0 0, calc(100% - 15px) 0, 100% 50%, calc(100% - 15px) 100%, 0 100%);
}

.chevron.last {
  padding-right: 1.2rem;
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%, 15px 50%);
}

.chevron-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.chevron-label {
  font-size: 0.7rem;
  font-weight: 700;
}

.chevron-sublabel {
  font-size: 0.6rem;
  margin-top: 0.2rem;
  opacity: 0.8;
}

.chevron-detail {
  font-size: 0.55rem;
  margin-top: 0.3rem;
  opacity: 0.6;
}

.details-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 0.8rem;
  margin-top: 1.5rem;
}

.detail-box {
  padding: 0.6rem;
  border-top: 2px solid;
  font-size: 0.65rem;
  color: #666;
  line-height: 1.5;
}

.detail-item {
  margin-bottom: 0.2rem;
}
</style>
