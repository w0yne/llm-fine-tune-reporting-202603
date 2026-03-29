<script setup>
defineProps({
  label: { type: String, default: 'Key Insight' },
  insight: { type: String, required: true },
  highlightColor: { type: String, default: '#0284c7' },
  soWhat: { type: String, default: '' }
})
</script>

<template>
  <div class="insight-slide">
    <div class="content">
      <div class="label">{{ label }}</div>
      <div class="insight" v-html="insight"></div>
      <div v-if="soWhat" class="so-what">
        <span v-html="soWhat"></span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.insight-slide {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 70%;
}

.content {
  max-width: 700px;
  text-align: center;
}

.label {
  font-size: 0.75rem;
  color: #999;
  text-transform: uppercase;
  letter-spacing: 0.15em;
  margin-bottom: 1.5rem;
}

.insight {
  font-size: 2.2rem;
  font-weight: 300;
  line-height: 1.4;
  color: #111;
}

.insight :deep(strong) {
  font-weight: 600;
}

.so-what {
  margin-top: 2.5rem;
  padding: 1rem 2rem;
  background: #f8fafc;
  border-radius: 8px;
  border-left: 4px solid #0284c7;
}

.so-what span {
  font-size: 0.85rem;
  color: #555;
  font-weight: 500;
}
</style>
