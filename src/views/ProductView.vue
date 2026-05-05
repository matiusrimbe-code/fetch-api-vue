<script setup>
import { onMounted, ref } from 'vue'
import { RouterLink, useRoute, useRouter } from 'vue-router'
import axios from 'axios'
import ProductForm from '@/components/ProductForm.vue'

const product = ref({})
const route = useRoute()
const router = useRouter()
const id = parseInt(route.params.id)

onMounted(() => {
  fetchData()
})

async function fetchData() {
  const API_URL = `http://localhost:3000/products/${id}`
  try {
    const response = await axios.get(API_URL)
    product.value = response.data
  } catch (error) {
    console.log(error)
  }
}

async function deleteProduct() {
  const API_URL = `http://localhost:3000/products/${id}`
  try {
    await axios.delete(API_URL)
    router.push({ name: 'home' })
  } catch (error) {
    console.log(error)
  }
}
</script>

<template>
  <div class="product-detail">
    <h2>{{ product.title }}</h2>
    <img :src="product.image" :alt="product.title" class="product-image" />
    <p>Description: {{ product.description }}</p>
    <p>Price: {{ product.price }}</p>
    <ProductForm />
    <RouterLink to="/" class="back-button">Back</RouterLink>
    <button @click="deleteProduct" class="delete-button">Delete</button>
  </div>
</template>

<style scoped>
.product-detail {
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
  text-align: center;
}

.product-image {
  max-width: 100%;
  height: auto;
  margin-bottom: 10px;
}

.product-detail p {
  margin-bottom: 5px;
}

.back-button {
  display: inline-block;
  padding: 8px 16px;
  background-color: #007bff;
  color: #fff;
  text-decoration: none;
  border: none;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.back-button:hover {
  background-color: #0056b3;
}

.delete-button {
  font-size: 16px;
  display: inline-block;
  padding: 8px 16px;
  margin-left: 10px;
  background-color: #dc3545;
  color: #fff;
  text-decoration: none;
  border: none;
  border-radius: 4px;
  transition: background-color 0.3s;
}

.delete-button:hover {
  background-color: #c82333;
  cursor: pointer;
}
</style>
