<script setup>
defineProps({
  title: { type: String, required: true },
  subtitle: { type: String, default: '' },
  tagline: { type: String, default: '' },
  variant: { type: String, default: 'cover' } // 'cover' | 'thank-you'
})
</script>

<template>
  <div class="cover-slide">
    <template v-if="variant === 'cover'">
      <h1 class="title">{{ title }}</h1>
      <div v-if="subtitle" class="subtitle">{{ subtitle }}</div>
      <div v-if="tagline" class="tagline">{{ tagline }}</div>
    </template>

    <template v-else-if="variant === 'thank-you'">
      <div class="thank-you-content">
        <div class="thank-you-title">{{ title }}</div>
        <div v-if="subtitle" class="thank-you-subtitle">{{ subtitle }}</div>
        <slot></slot>
      </div>
    </template>
  </div>
</template>

<style scoped>
.cover-slide {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
  padding: 2rem;
}

.title {
  font-size: 2.8rem;
  font-weight: 700;
  color: #111;
  margin: 0;
  line-height: 1.2;
}

.subtitle {
  font-size: 1.6rem;
  color: #666;
  margin-top: 1rem;
  font-weight: 300;
}

.tagline {
  margin-top: 3rem;
  font-size: 0.95rem;
  color: #999;
}

.thank-you-content {
  max-width: 700px;
}

.thank-you-title {
  font-size: 1.8rem;
  font-weight: 300;
  color: #333;
  margin-bottom: 1rem;
}

.thank-you-subtitle {
  font-size: 1rem;
  color: #888;
  margin-bottom: 3rem;
}
</style>
