<script setup>
import { RouterLink, RouterView } from 'vue-router'
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
  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

a {
  text-decoration: none;
  color: #000;
  font-weight: bold;
}

a:hover {
  color: #fd4c00;
}

.router-link-active {
  color: #fd4c00;
}

h1 {
  font-size: clamp(2rem, 4vw + 1rem, 4rem);
  text-align: center;
  font-weight: 900;
  font-family: 'Raleway', sans-serif;
  background: -webkit-linear-gradient(right, #fd4c00, yellow);
  background: -o-linear-gradient(right, #fd4c00, yellow);
  background: -moz-linear-gradient(right, #fd4c00, yellow);
  background: linear-gradient(to right, #fd4c00, yellow);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

nav {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin: 2rem 0;
}

.wrapper {
  max-width: 100%;
  margin: 1rem;
}
</style>
