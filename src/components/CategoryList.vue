<script setup>
import { ref } from 'vue';
import ProductItem from './ProductItem.vue';

const products = ref([]);
const urlProducts = 'https://67414054e4647499008d305b.mockapi.io/api/v1/products';

async function getProducts() {
  products.value = await (await fetch(urlProducts)).json();
}


const formatCurrency = (amount) => {
  return new Intl.NumberFormat('vi-VN').format(amount) + '.000đ'; // Thêm đuôi .000đ vào cuối
};

getProducts();
</script>

<template>
  <div class="container">
    <h1>Danh sách sản phẩm</h1>
    <div class="row">
      <div class="col-3 g-3" v-for="product in products" :key="product.id">
        <ProductItem :id="product.id">
          <template #productName>{{ product.name }}</template>
          <template #productPrice>{{ formatCurrency(product.price) }}</template>
          <template #productImage>
            <img :src="product.image" alt="product image" width="100%" />
          </template>
        </ProductItem>
      </div>
    </div>
  </div>
</template>
