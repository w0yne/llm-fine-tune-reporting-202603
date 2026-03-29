<script setup>
defineProps({
  title: { type: String, default: '' },
  subtitle: { type: String, default: '' }
})
</script>

<template>
  <div class="slide-heading">
    <h1 v-if="title" class="title">{{ title }}</h1>
    <div v-if="subtitle" class="subtitle">{{ subtitle }}</div>
  </div>
</template>

<style scoped>
.slide-heading {
  margin-bottom: 1rem;
}

.title {
  font-size: 1.75rem;
  font-weight: 700;
  margin: 0;
  line-height: 1.2;
}

.subtitle {
  font-size: 0.85rem;
  color: #666;
  margin-top: 0.3rem;
}
</style>
