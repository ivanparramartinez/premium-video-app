<script setup>
import { ref, toRaw } from 'vue'

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
  },
  modeCart: {
    type: Boolean,
    default: false
  }
})

const transactionMode = ref(null)
const date = ref(null)
const quantity = ref(null)
const added = ref(false)

const emit = defineEmits(['addToCart', 'removeFromCart'])

function changeMode(mode) {
  if (mode === 'rent') {
    transactionMode.value = 'rent'
  } else if (mode === 'buy') {
    transactionMode.value = 'buy'
  } else {
    transactionMode.value = null
  }
}

function addToCart(movie, mode, date, quantity) {
  if (
    (mode === 'rent' && (date == null || quantity == null || quantity < 1)) ||
    (mode === 'buy' && (quantity < 1 || !quantity))
  ) {
    alert(mode === 'rent' ? 'Por favor introduce fecha y cantidad' : 'Por favor introduce cantidad')
    return
  }
  emit('addToCart', toRaw(movie), mode, date, quantity)
  added.value = true
}

function removeFromCart(movie) {
  emit('removeFromCart', toRaw(movie))
}
</script>

<template>
  <div class="grid-card-container">
    <div class="grid-card-left">
      <img :alt="movie.Title" :src="movie.Poster" v-if="movie.Poster !== 'N/A'" />
      <img src="@/assets/no-image.jpg" alt="" v-else />
    </div>
    <div class="grid-card-right">
      <div class="movie-description">
        <h2 class="title">{{ movie.Title }}</h2>
        <p class="year">{{ movie.Year }}</p>
      </div>
      <div :class="movie.Type === 'movie' ? 'bubble-movie' : 'bubble-series'">
        <p class="type">{{ movie.Type }}</p>
      </div>
      <div class="movie-transaction-details" v-if="modeCart">
        <p><strong>Transacción: </strong>{{ movie.mode === 'rent' ? 'Renta' : 'Compra' }}</p>
        <p v-if="movie.mode === 'rent'"><strong>Fecha: </strong>{{ movie.date }}</p>
        <p><strong>Cantidad: </strong>{{ movie.quantity }}</p>
      </div>
      <div class="mode-rent" v-if="transactionMode != null && !added">
        <input type="date" v-model="date" v-if="transactionMode === 'rent'" />
        <input type="number" placeholder="Cantidad..." v-model="quantity" />
        <div class="movie-buttons">
          <button
            :class="transactionMode === 'rent' ? 'rent-button' : 'buy-button'"
            v-if="allowAddToCart"
            @click="addToCart(movie, transactionMode, date, quantity)"
          >
            {{ transactionMode === 'rent' ? 'Rentar' : 'Comprar' }}
          </button>
          <button class="cancel-button" @click="changeMode(null)">Cancelar</button>
        </div>
      </div>
      <div class="movie-buttons" v-else>
        <button class="rent-button" v-if="allowAddToCart" @click="changeMode('rent')">
          Rentar
        </button>
        <button class="buy-button" v-if="allowAddToCart" @click="changeMode('buy')">Comprar</button>
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
  grid-template-columns: 40% 60%;
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

.movie-transaction-details {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 1rem;
  width: 100%;
}

.movie-transaction-details p {
  font-weight: 300;
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

.cancel-button {
  background-color: #000000;
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

.mode-rent {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  width: 100%;
}

input {
  border-radius: 5px;
  border: none;
  width: 100%;
  font-size: 0.8rem;
  outline: none;
}
</style>
