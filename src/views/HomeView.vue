<script setup>
import Pagination from '@/components/Pagination.vue';
import ProductCard from '@/components/ProductCard.vue';
import { onBeforeMount, onBeforeUnmount, onBeforeUpdate, onMounted, onUnmounted, onUpdated, ref } from 'vue';

const page = ref(1)

function nextPage() {
  page.value++
}

onBeforeMount(() => {
  console.log('On Before Mount')
})

onMounted(() => {
  console.log('On Mounted')
})

onBeforeUpdate(() => {
  console.log('On Before Update')
})

onUpdated(() => {
  console.log('On Updated')
})

onBeforeUnmount(() => {
  console.log('ON Before Unmount')
})

onUnmounted(() => {
  console.log('On Unmounted')
})
</script>

<template>
  {{ page }}

  <button @click="nextPage">Next Page</button>
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