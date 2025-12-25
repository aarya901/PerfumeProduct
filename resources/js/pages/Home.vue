<template>
  <section class="hero">
    <h1>{{ title }}</h1>
    <p>{{ tagline }}</p>
    <button @click="changeText">Explore</button>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const title = ref('Luxury Perfumes')
const tagline = ref('Minimal. Elegant. Long-lasting fragrance.')

const changeText = () => {
  tagline.value = 'Crafted for modern elegance.'
}
</script>

<style scoped>
.hero {
  padding:80px;
  background:#f7f3ef;
  text-align:center;
}
button {
  margin-top:20px;
  padding:10px 16px;
}
</style>
