<script setup>
import { ref } from 'vue';

const props = defineProps(['id']);
console.log(props);

const id = props.id;
const urlDetailProduct = 'https://67414054e4647499008d305b.mockapi.io/api/v1/products/' + id;
const product = ref({});

async function getProduct() {
  product.value = await (await fetch(urlDetailProduct)).json();
}


const formatCurrency = (amount) => {
  return new Intl.NumberFormat('vi-VN').format(amount) + '.000đ'; 
};

getProduct();
</script>

<template>
  <h2>{{ name }}</h2>
  <div class="container">
    <h1>{{ product.name }} - {{ product.id }}</h1>
    <p>Quantity: {{ product.quantity }}</p>
    <p>Price: {{ formatCurrency(product.price) }}</p> 
    <p>{{ product.description }}</p>
  </div>
</template>
