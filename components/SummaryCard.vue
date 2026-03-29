<script setup>
defineProps({
  number: { type: [String, Number], required: true },
  title: { type: String, required: true },
  description: { type: String, default: '' },
  color: { type: String, default: '#0284c7' }
})
</script>

<template>
  <div class="summary-card">
    <div class="number" :style="{ color }">{{ number }}</div>
    <div class="content">
      <div class="title">{{ title }}</div>
      <div v-if="description" class="description">{{ description }}</div>
    </div>
  </div>
</template>

<style scoped>
.summary-card {
  display: flex;
  gap: 1rem;
  padding: 0.8rem 1.2rem;
  border: 1px solid #e5e7eb;
  border-radius: 10px;
}

.number {
  font-size: 1.6rem;
  font-weight: 700;
  min-width: 36px;
}

.content {
  flex: 1;
}

.title {
  font-size: 1rem;
  font-weight: 600;
}

.description {
  font-size: 0.72rem;
  color: #888;
  margin-top: 0.2rem;
  line-height: 1.4;
}
</style>
