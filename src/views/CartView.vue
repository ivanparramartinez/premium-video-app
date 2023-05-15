<script setup>
import { onBeforeMount, ref } from 'vue'
import CompMovieCard from '@/components/CompMovieCard.vue'

const cart = ref([])

const removeFromCart = (movie) => {
  cart.value = cart.value.filter((m) => m.imdbID !== movie.imdbID)
  localStorage.setItem('cart', JSON.stringify(cart.value))
}

const clearCart = () => {
  cart.value = []
  localStorage.setItem('cart', JSON.stringify(cart.value))
}

onBeforeMount(() => {
  let localCart = JSON.parse(localStorage.getItem('cart'))

  if (!localCart) {
    localStorage.setItem('cart', JSON.stringify([]))
  }

  cart.value = JSON.parse(localStorage.getItem('cart'))
})
</script>
<template>
  <div class="clearCartButton" v-if="cart.length > 0">
    <button class="clear-button" @click="clearCart()">Vaciar carrito de compra</button>
  </div>
  <div class="grid-container-cart">
    <comp-movie-card
      v-for="(movie, idx) in cart"
      :key="idx"
      :movie="movie"
      allow-remove-from-cart
      @removeFromCart="removeFromCart"
    />
  </div>
</template>

<style scoped>
.grid-container-cart {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(min(18rem, 100%), 1fr));
  justify-items: center; /* Centrar los elementos horizontalmente */
  grid-auto-rows: 1fr;
  gap: 1rem;
}

.clearCartButton {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 1rem;
}

.clear-button {
  background-color: #f44336;
  color: white;
  padding: 0.5rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>
