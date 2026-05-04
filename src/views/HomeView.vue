<script setup>
import Pagination from '@/components/Pagination.vue';
import ProductCard from '@/components/ProductCard.vue';
import { onBeforeMount, onMounted } from 'vue';

onBeforeMount(() => {
  console.log('On Before Mount')
})

onMounted(() => {
  console.log('On Mounted')
})

</script> 

<template>
  <div class="product-grid">
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