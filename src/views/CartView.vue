<script setup>
const cart = JSON.parse(localStorage.getItem('cart'));
</script>
<template>
  <div class="grid">
    <div v-for="(movie, idx) in cart" :key="idx">
      <div>
        <img :src="movie.Poster" alt="movie.Title"/>
        <h3>{{
            movie.Title
          }}</h3>
      </div>
    </div>
  </div>
</template>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 1rem;
  justify-content: center;
}
</style>

