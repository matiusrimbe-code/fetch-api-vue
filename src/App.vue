<script setup>
import { RouterView } from 'vue-router'
import HomeView from './views/HomeView.vue';
</script>

<template>
  <main class="container">
    <Suspense>
      <template #default>
        <HomeView />
        <!-- <RouterView /> -->
      </template>
      <template #fallback>
        <p>Loading ...</p>
      </template>
    </Suspense>
  </main>
</template>

<style scoped>
.container {
  width: 80%;
  margin: 0 auto;
}
</style>
