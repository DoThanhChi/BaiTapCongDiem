<script setup>
import { ref, onMounted } from 'vue';


const cart = ref({});

onMounted(() => {
  const storedCart = localStorage.getItem('cart');
  if (storedCart) {
    cart.value = JSON.parse(storedCart);
    console.log(cart.value);  
  }
});
</script>

<template>
  <div class="container">
    <h1>Giỏ hàng của bạn</h1>
    <table class="table">
      <thead>
        <tr>
          <th>Ảnh</th>
          <th>ID Sản phẩm</th> 
          <th>Số lượng</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, id) in cart" :key="id">
          <td>
            <img :src="item.image || 'https://placehold.co/100'" alt="Product Image" width="50" />
          </td>
          <td>{{ `Sản phẩm ${id}` }}</td> 
          <td>{{ item.quantity }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
