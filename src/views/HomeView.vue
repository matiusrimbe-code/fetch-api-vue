<script setup>
import Pagination from '@/components/Pagination.vue';
import ProductCard from '@/components/ProductCard.vue';
import { ref } from 'vue';
import axios from 'axios';

const products = ref([]);

async function getProducts() {
  const response = await axios.get('http://localhost:3000/products');
  products.value = response.data
}

getProducts();

</script>

<template>
  <div class="product-grid">
    {{ products }}
    <ProductCard />
  </div>
  <div class="pagination">
    <Pagination />
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