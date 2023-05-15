<script setup>
import { toRaw } from 'vue'

defineProps({
  movie: {
    type: Object,
    required: true
  },
  allowAddToCart: {
    type: Boolean,
    default: false
  },
  allowRemoveFromCart: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['addToCart', 'removeFromCart'])

function addToCart(movie) {
  emit('addToCart', toRaw(movie))
}

function removeFromCart(movie) {
  emit('removeFromCart', toRaw(movie))
}
</script>

<template>
  <div class="grid-card-container">
    <div class="grid-card-left">
      <img :alt="movie.Title" :src="movie.Poster" v-if="movie.Poster" />
    </div>
    <div class="grid-card-right">
      <div class="movie-description">
        <h2 class="title">{{ movie.Title }}</h2>
        <p class="year">{{ movie.Year }}</p>
      </div>
      <div :class="movie.Type === 'movie' ? 'bubble-movie' : 'bubble-series'">
        <p class="type">{{ movie.Type }}</p>
      </div>
      <div class="movie-buttons">
        <button class="rent-button" v-if="allowAddToCart" @click="addToCart(movie)">Rentar</button>
        <button class="buy-button" v-if="allowAddToCart" @click="addToCart(movie)">Comprar</button>
        <button class="remove-button" v-if="allowRemoveFromCart" @click="removeFromCart(movie)">
          Remove from Cart
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.grid-card-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  width: auto;
  height: auto;
  background-color: #f1f1f1;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

.grid-card-left img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.grid-card-right {
  display: flex;
  padding: 1rem;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1rem;
}

.movie-description {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  gap: 0.5rem;
}

.movie-description h2 {
  margin: 0;
  font-size: 1rem;
  font-weight: bold;
}

.movie-description p {
  font-size: 0.8rem;
}

.movie-buttons {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  width: 100%;
}

.rent-button {
  background-color: #4caf50;
  color: white;
  padding: 0.5rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.buy-button {
  background-color: #2196f3;
  color: white;
  padding: 0.5rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.remove-button {
  background-color: #f44336;
  color: white;
  padding: 0.5rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  transform: scale(1.01);
}

.bubble-movie {
  border-radius: 20px;
  border: 1px solid #002ee5;
  color: #002ee5;
  font-size: 0.8rem;
  font-weight: bold;
  padding: 0.5rem;
  width: fit-content;
}

.bubble-series {
  border-radius: 20px;
  border: 1px solid #ff0000;
  color: #ff0000;
  font-size: 0.8rem;
  font-weight: bold;
  padding: 0.5rem;
  width: fit-content;
}
</style>
