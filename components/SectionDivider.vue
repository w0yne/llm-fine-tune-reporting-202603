<script setup>
defineProps({
  section: { type: String, required: true },
  title: { type: String, required: true },
  subtitle: { type: String, default: '' }
})
</script>

<template>
  <div class="section-divider">
    <div class="section-label">{{ section }}</div>
    <h1 class="section-title">{{ title }}</h1>
    <div v-if="subtitle" class="section-subtitle">{{ subtitle }}</div>
  </div>
</template>

<style scoped>
.section-divider {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100%;
}

.section-label {
  font-size: 0.9rem;
  color: #999;
  text-transform: uppercase;
  letter-spacing: 0.15em;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin: 0.5rem 0;
}

.section-subtitle {
  font-size: 1.1rem;
  color: #666;
  margin-top: 1rem;
  font-weight: 300;
}
</style>
