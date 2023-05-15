<script setup>
import { onBeforeMount, ref, watch, toRaw } from 'vue'
import axios from 'axios'
import CompMovieCard from '@/components/CompMovieCard.vue'

const uri = 'http://www.omdbapi.com/?apikey=5eec5adc&'

const search = ref('')
const movies = ref([])
const cart = ref([])

const getMovies = async () => {
  const res = await axios.get(`${uri}s=${search.value}`)
  if (res.data.Search) {
    movies.value = res.data.Search
  } else {
    movies.value = []
  }
}

const addToCart = (movie) => {
  let found = cart.value.find((m) => m.imdbID === movie.imdbID)
  if (found) {
    alert('Ya agregaste esta película al carrito')
  } else {
    cart.value.push(movie)
    localStorage.setItem('cart', JSON.stringify(cart.value))
  }
}

onBeforeMount(() => {
  let localCart = JSON.parse(localStorage.getItem('cart'))

  if (!localCart) {
    localStorage.setItem('cart', JSON.stringify([]))
  }

  cart.value = JSON.parse(localStorage.getItem('cart'))
})

watch([() => search.value, () => movies.value], ([newVal1, newVal2]) => {
  if (newVal1.length > 3 && toRaw(newVal2).length === 0) {
    alert('No se encontraron resultados')
    search.value = ''
  }
})
</script>

<template>
  <main>
    <input v-model="search" type="text" @input="getMovies" placeholder="Buscar película..." />
    <div class="grid-container">
      <comp-movie-card
        v-for="(movie, idx) in movies"
        :key="idx"
        :movie="movie"
        allow-add-to-cart
        @addToCart="addToCart"
      />
    </div>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
}

.grid-container {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(min(18rem, 100%), 1fr));
  grid-auto-rows: 1fr;
  gap: 1rem;
}

input {
  padding: 1rem;
  outline: none;
  font-family: 'Raleway', sans-serif;
  border: solid 0.2rem transparent;
  border-radius: 1.5rem;
  background-image: linear-gradient(white, white), linear-gradient(to right, #fd4c00, yellow);
  background-origin: border-box;
  background-clip: padding-box, border-box;
}
</style>
