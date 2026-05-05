<script setup>
import Pagination from '@/components/Pagination.vue'
import ProductCard from '@/components/ProductCard.vue'
import { onMounted, ref, watch } from 'vue'
import axios from 'axios'

const page = ref(1)
const perPage = ref(8)
const products = ref([])

onMounted(async () => {
  products.value = await axios
    .get(`http://localhost:3000/products?_page=${page.value}&_per_page=${perPage.value}`)
    .then((res) => res.data)
})

watch(page, async () => {
  products.value = await axios
    .get(`http://localhost:3000/products?_page=${page.value}&_per_page=${perPage.value}`)
    .then((res) => res.data)
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
  <div class="product-grid">
    <ProductCard v-for="product in products.data" :key="product.id" :product="product" />
  </div>

  <div class="pagination">
    <Pagination :page="page" :totalPages="products.pages" @changePage="changePage" />
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
</style>
