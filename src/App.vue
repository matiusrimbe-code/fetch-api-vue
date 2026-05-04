<script setup>
import { RouterView, RouterLink } from 'vue-router'
import Navigation from './components/Navigation.vue';
</script>

<template>
  <header class="container">
    <Navigation />
  </header>
  <main class="container">
    <RouterView />
  </main>
</template>

<style scoped>
.container {
  width: 80%;
  margin: 0 auto;
}
</style>
