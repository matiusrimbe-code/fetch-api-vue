<script setup>
import Pagination from '@/components/Pagination.vue'
import ProductCard from '@/components/ProductCard.vue'
import { ref, watchEffect } from 'vue'
import axios from 'axios'

const page = ref(1)
const perPage = ref(6)
const products = ref([])
const isLoading = ref(true)

async function fetchData() {
  const API_URL = `http://localhost:3000/products?_page=${page.value}&_per_page=${perPage.value}`
  try {
    isLoading.value = true
    const response = await axios.get(API_URL)
    products.value = response.data
  } catch (error) {
    console.log(error)
  } finally {
    isLoading.value = false
  }
}

watchEffect(() => {
  fetchData()
})

function changePage(newPage) {
  if (newPage < 1) {
    newPage = 1
  }

  if (newPage > products.value.pages) {
    newPage = products.value.pages
  }

  page.value = newPage
}
</script>

<template>
  <div v-if="isLoading">
    <p class="loading">Loading ...</p>
  </div>
  <div v-else>
    <div class="product-grid">
      <ProductCard v-for="product in products.data" :key="product.id" :product="product" />
    </div>

    <div class="pagination">
      <Pagination :page="page" :totalPages="products.pages" @changePage="changePage" />
    </div>
  </div>
</template>

<style scoped>
.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
  margin: 0 auto;
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.loading {
  text-align: center;
}
</style>
