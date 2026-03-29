<script setup>
defineProps({
  number: { type: [String, Number], required: true },
  title: { type: String, required: true },
  description: { type: String, default: '' }
})
</script>

<template>
  <div class="agenda-card">
    <div class="number">{{ String(number).padStart(2, '0') }}</div>
    <div class="title">{{ title }}</div>
    <div v-if="description" class="description" v-html="description"></div>
  </div>
</template>

<style scoped>
.agenda-card {
  text-align: center;
  padding: 1.8rem 1rem;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
}

.number {
  font-size: 2.2rem;
  font-weight: 700;
  color: #000;
}

.title {
  font-size: 1rem;
  font-weight: 600;
  margin-top: 0.5rem;
}

.description {
  font-size: 0.8rem;
  color: #888;
  margin-top: 0.3rem;
  line-height: 1.4;
}
</style>
