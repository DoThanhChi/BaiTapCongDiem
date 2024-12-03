<script setup>
import { ref } from 'vue';
import ProductItem from './ProductItem.vue';

const products = ref([]);
const urlProducts = 'https://67414054e4647499008d305b.mockapi.io/api/v1/products';

async function getProducts() {
  products.value = await (await fetch(urlProducts)).json();
}
getProducts();


const formatCurrency = (amount) => {
 
  const formattedAmount = (amount >= 1000 ? amount / 1000 : amount).toLocaleString();
  return `${formattedAmount}0.VNĐ`; 
};
</script>

<template>
  <div class="container">

    <h1>Danh sách sản phẩm</h1>
    <RouterLink to="/cart" class="btn btn-primary">
  Đi đến giỏ hàng
</RouterLink>
    <div class="row">
      <div class="col-3 g-3" v-for="product in products" :key="product.id">
        <ProductItem :id="product.id">
          <template #productName>{{ product.name }}</template>
          <template #productPrice>{{ formatCurrency(product.price) }}</template>
        </ProductItem>
      </div>
    </div>
  </div>
</template>
