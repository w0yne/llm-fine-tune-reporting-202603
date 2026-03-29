<script setup>
defineProps({
  columns: { type: Number, default: 3 },
  variant: { type: String, default: 'agenda' } // 'agenda' | 'summary' | 'appendix'
})
</script>

<template>
  <div
    class="card-grid"
    :class="[`variant-${variant}`]"
    :style="{ gridTemplateColumns: `repeat(${columns}, 1fr)` }"
  >
    <slot></slot>
  </div>
</template>

<style scoped>
.card-grid {
  display: grid;
  gap: 1.5rem;
  margin-top: 1rem;
}

.variant-agenda {
  gap: 1.5rem;
}

.variant-summary {
  grid-template-columns: 1fr !important;
  gap: 0.5rem;
  margin-top: 0.8rem;
}

.variant-appendix {
  gap: 1.2rem;
}
</style>
