<template>
  <section class="products">
    <h2>Our Collection</h2>

    <div class="grid">
      <div class="card" v-for="p in perfumes" :key="p.id">
        <img :src="p.image" />
        <h3>{{ p.name }}</h3>
        <p>Rs {{ p.price }}</p>

        <button @click="addToCart">
          Add to Cart
        </button>
      </div>
    </div>

    <p class="cart">
      Cart Items: {{ cartCount }}
    </p>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const cartCount = ref(0)

const perfumes = ref([
  { id: 1, name: 'Rose Oud', price: 2500, image: '/images/p1.png' },
  { id: 2, name: 'Amber Night', price: 3200, image: '/images/p2.png' },
  { id: 3, name: 'Fresh Citrus', price: 1800, image: '/images/p3.png' }
])

const addToCart = () => {
  cartCount.value++
}
</script>

<style scoped>
.products {
  padding:40px;
}
.grid {
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:20px;
}
.card {
  background:#fff;
  padding:20px;
  border-radius:10px;
  text-align:center;
}
button {
  margin-top:10px;
  padding:8px 12px;
  border:none;
  background:#000;
  color:#fff;
  cursor:pointer;
}
.cart {
  margin-top:20px;
  font-weight:bold;
}
</style>
