<script setup>
import { ref } from 'vue';
import { BIconCart, BIconEye } from 'bootstrap-icons-vue';

const props = defineProps(['id', 'name', 'price']);

const images = [
  "https://via.placeholder.com/150/0000FF/808080?text=Smart",
  "https://via.placeholder.com/150/FF0000/FFFFFF?text=Laptop",
  "https://via.placeholder.com/150/00FF00/000000?text=Headphones",
  "https://via.placeholder.com/150/FFFF00/000000?text=Smartwatch"
];

const imageUrl = images[props.id % images.length]; 

const urlDetail = "/product/" + props.id;

function addToCart() {
  let cart = localStorage.getItem('cart');
  cart = JSON.parse(cart);
  if (!cart) {
    cart = {};  
  }

  if (!cart[props.id]) {
    cart[props.id] = {
      name: props.name,
      price: parseFloat(props.price),
      image: imageUrl, 
      quantity: 1,
    };
  } else {
    cart[props.id].quantity += 1;
  }

  localStorage.setItem('cart', JSON.stringify(cart));
  alert('Sản phẩm đã được thêm vào giỏ hàng');
}
</script>

<template>
  <div class="card">
    <img class="card-img-top" :src="imageUrl" alt="Product Image" width="100%" />
    <div class="card-body">
      <h4 class="card-title">
        <slot name="productName">{{ props.name }}</slot>
      </h4>
      <p class="card-text">
        <slot name="productPrice">{{ props.price }}</slot>
      </p>
      <RouterLink :to="urlDetail" class="btn btn-success">
        <BIconEye />
      </RouterLink>
      <button class="btn btn-warning ml-2" @click="addToCart">
        <BIconCart />
        Thêm vào giỏ hàng
      </button>
    </div>
  </div>
</template>
