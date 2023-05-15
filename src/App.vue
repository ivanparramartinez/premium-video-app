<script setup>
import {RouterLink, RouterView} from 'vue-router';
</script>

<template>
  <header>
    <div class="wrapper">
      <h1 class="gradient-text">Premium Video</h1>
      <nav>
        <RouterLink to="/">Búsqueda</RouterLink>
        <RouterLink to="/cart">Carrito de Compras</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView/>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

h1 {
  font-size: clamp(2rem, 4vw + 1rem, 6rem);
  text-align: center;
  font-weight: 900;
  font-family: 'Raleway', sans-serif;
  background: -webkit-linear-gradient(right, #00c4ff, #ff0091);
  background: -o-linear-gradient(right, #00c4ff, #ff0091);
  background: -moz-linear-gradient(right, #00c4ff, #ff0091);
  background: linear-gradient(to right, #00c4ff, #ff0091);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

nav {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-top: 2rem;
}

.wrapper {
  max-width: 100%;
  margin: 0 auto;
  padding: 0 2rem;
}
</style>
