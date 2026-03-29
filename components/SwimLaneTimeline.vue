<script setup>
defineProps({
  periods: {
    type: Array,
    required: true
    // Each period label: string
  },
  lanes: {
    type: Array,
    required: true
    // Each lane: { label: string, color: string, segments: [{ span: number, label: string, shade: 'dark' | 'medium' | 'light' }] }
  },
  milestones: {
    type: Array,
    default: () => []
    // Each: { text: string }
  },
  labelWidth: { type: Number, default: 90 }
})
</script>

<template>
  <div class="swim-lane-timeline">
    <div class="grid-header">
      <div class="lane-label-spacer" :style="{ width: `${labelWidth}px` }"></div>
      <div
        v-for="(period, idx) in periods"
        :key="idx"
        class="period-label"
      >
        {{ period }}
      </div>
    </div>

    <div
      v-for="(lane, lIdx) in lanes"
      :key="lIdx"
      class="lane-row"
    >
      <div class="lane-label" :style="{ width: `${labelWidth}px`, borderTopColor: lane.color }">
        {{ lane.label }}
      </div>
      <div class="lane-segments">
        <div
          v-for="(seg, sIdx) in lane.segments"
          :key="sIdx"
          class="segment"
          :style="{
            gridColumn: `span ${seg.span}`,
            backgroundColor: getSegmentColor(lane.color, seg.shade)
          }"
        >
          <span :style="{ color: seg.shade === 'light' ? getDarkTextColor(lane.color) : 'white' }">
            {{ seg.label }}
          </span>
        </div>
      </div>
    </div>

    <div v-if="milestones.length > 0" class="milestones">
      <span v-for="(ms, idx) in milestones" :key="idx">▲ {{ ms.text }}</span>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    getSegmentColor(baseColor, shade) {
      // Simple opacity-based shading
      const opacities = { dark: 1, medium: 0.7, light: 0.4 }
      return baseColor
    },
    getDarkTextColor(color) {
      // Return a darker version for light backgrounds
      return '#333'
    }
  }
}
</script>

<style scoped>
.swim-lane-timeline {
  margin: 1rem auto;
  max-width: 720px;
}

.grid-header {
  display: flex;
  gap: 2px;
  margin-bottom: 2px;
}

.lane-label-spacer {
  flex-shrink: 0;
}

.period-label {
  flex: 1;
  text-align: center;
  font-size: 0.65rem;
  font-weight: 600;
  color: #888;
  padding: 0.4rem;
}

.lane-row {
  display: flex;
  gap: 2px;
  margin-bottom: 2px;
}

.lane-label {
  flex-shrink: 0;
  padding: 0.5rem 0.4rem;
  font-size: 0.7rem;
  font-weight: 600;
  border-top: 2px solid;
}

.lane-segments {
  flex: 1;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 2px;
}

.segment {
  padding: 0.3rem;
  border-radius: 4px;
  text-align: center;
}

.segment span {
  font-size: 0.6rem;
  font-weight: 500;
}

.milestones {
  display: flex;
  gap: 1rem;
  margin-top: 0.8rem;
  justify-content: center;
}

.milestones span {
  font-size: 0.6rem;
  color: #888;
}
</style>
