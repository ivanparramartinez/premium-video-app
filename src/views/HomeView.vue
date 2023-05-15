<script setup>
import { onBeforeMount, ref, watch } from 'vue'
import axios from 'axios'
import CompMovieCard from '@/components/CompMovieCard.vue'

const uri = `https://www.omdbapi.com/?apikey=${import.meta.env.VITE_OMDB_API_KEY}&`

const search = ref('')
const movies = ref([])
const cart = ref([])
let timeoutId = null

const getMovies = async () => {
  await axios.get(`${uri}s=${search.value}`).then((res) => {
    if (res.data.Search) {
      movies.value = res.data.Search
    } else {
      alert('Error al obtener el listado. Intente nuevamente')
      search.value = ''
      movies.value = []
    }
  })
}

function handleInput() {
  clearTimeout(timeoutId)
  timeoutId = setTimeout(() => {
    if (search.value.length > 3) {
      getMovies()
    }
  }, 1500)
}

const addToCart = (movie, mode, date, quantity) => {
  console.log(mode, date, quantity)
  let found = cart.value.find((m) => m.imdbID === movie.imdbID)
  if (found) {
    alert('Ya agregaste esta película al carrito')
  } else {
    movie.mode = mode
    movie.date = date
    movie.quantity = quantity
    cart.value.push(movie)
    localStorage.setItem('cart', JSON.stringify(cart.value))
    alert('Película agregada al carrito')
  }
}

watch(search, () => {
  if (search.value === '') {
    movies.value = []
  }
})

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
    <input
      v-model="search"
      type="text"
      @input="handleInput"
      @keyup.esc="search = ''"
      placeholder="Buscar película..."
    />
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
  width: 40%;
  padding: 1rem;
  outline: none;
  font-family: 'Raleway', sans-serif;
  border: solid 0.2rem transparent;
  border-radius: 1.5rem;
  background-image: linear-gradient(white, white), linear-gradient(to right, #fd4c00, yellow);
  background-origin: border-box;
  background-clip: padding-box, border-box;
}

@media (max-width: 768px) {
  input {
    width: 80%;
  }
}
</style>
