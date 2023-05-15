<script setup>
import { onBeforeMount, ref } from 'vue'
import axios from 'axios'

const uri = 'http://www.omdbapi.com/?apikey=5eec5adc&'

const search = ref('')
const movies = ref([])
const movie = ref({})
const cart = ref([])

const getMovies = async () => {
  const res = await axios.get(`${uri}s=${search.value}`)
  movies.value = res.data.Search
}

const getMovie = async (id) => {
  const res = await axios.get(`${uri}i=${id}`)
  movie.value = res.data
}

const addToCart = (movie) => {
  cart.value.push(movie)
  localStorage.setItem('cart', JSON.stringify(cart.value))
}

const removeFromCart = (movie) => {
  cart.value = cart.value.filter((item) => item.imdbID !== movie.imdbID)
}

const clearCart = () => {
  cart.value = []
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
  <main>
    <input v-model="search" type="text" @input="getMovies" />
    <div class="grid-container">
      <div class="grid-card" v-for="(movie, idx) in movies" :key="idx">
          <img :src="movie.Poster" alt="movie.Title" />
          <h3>{{ movie.Title }}</h3>
          <button @click="addToCart(movie)">Add to Cart</button>
      </div>
    </div>
  </main>
  <!--  <main>
    <input v-model="search" type="text" @input="getMovies" />
    <div class="grid-container">
      <div v-for="(movie, idx) in movies" :key="idx">
        <div>
          <img :src="movie.Poster" alt="movie.Title" />
          <h3>{{ movie.Title }}</h3>
          <button @click="addToCart(movie)">Add to Cart</button>
        </div>
      </div>
    </div>
  </main>-->
</template>

<style scoped>
main {
  border: 1px solid blue;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
