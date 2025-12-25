<template>
  <section class="products">
    <h2>Products</h2>

    <p v-if="loading">Loading products...</p>

    <div class="grid">
      <div class="card" v-for="product in products" :key="product.id">
        <img :src="product.image" />
        <h4>{{ product.title }}</h4>
        <p>Rs {{ (product.price * 130).toFixed(0) }}</p>

        <button @click="addToCart(product)">
          Add to Cart
        </button>
      </div>
    </div>

    <!-- CART SECTION -->
    <div class="cart">
      <h3>🛒 Cart</h3>

      <p v-if="cart.length === 0">Cart is empty</p>

      <div v-for="item in cart" :key="item.id" class="cart-item">
        <img :src="item.image" />
        <div>
          <p>{{ item.title }}</p>
          <p>Qty: {{ item.qty }}</p>
          <p>Rs {{ (item.price * 130 * item.qty).toFixed(0) }}</p>
        </div>
      </div>

      <h4 v-if="cart.length > 0">
        Total: Rs {{ totalPrice }}
      </h4>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'
import axios from 'axios'

const products = ref([])
const cart = ref([])
const loading = ref(true)

const fetchProducts = async () => {
  try {
    const res = await axios.get('https://fakestoreapi.com/products')
    products.value = res.data.slice(0, 8)
  } catch (err) {
    console.error(err)
  } finally {
    loading.value = false
  }
}

const addToCart = (product) => {
  const item = cart.value.find(p => p.id === product.id)

  if (item) {
    item.qty += 1   // 👈 same product → increase quantity
  } else {
    cart.value.push({
      ...product,
      qty: 1
    })
  }
}

const totalPrice = computed(() => {
  return cart.value.reduce((sum, item) => {
    return sum + item.price * item.qty * 130
  }, 0).toFixed(0)
})

onMounted(fetchProducts)
</script>

<style scoped>
.products {
  padding:40px;
}
.grid {
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:20px;
}
.card {
  background:#fff;
  padding:15px;
  border-radius:10px;
  text-align:center;
}
img {
  height:100px;
  object-fit:contain;
}
button {
  margin-top:10px;
  padding:8px 12px;
  background:#000;
  color:#fff;
  border:none;
  cursor:pointer;
}
.cart {
  margin-top:40px;
  padding:20px;
  background:#f7f7f7;
  border-radius:10px;
}
.cart-item {
  display:flex;
  gap:15px;
  margin-bottom:15px;
}
.cart-item img {
  width:60px;
}
</style>
