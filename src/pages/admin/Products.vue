<template>
  <table>
    <thead>
      <tr>
        <th></th>
        <th>Title</th>
        <th>Image</th>
        <th>Actions</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="product in products" :key="product.id">
        <td>{{ product.id }}</td>
        <td>{{ product.title }}</td>
        <td><img :src="product.image" :alt="product.title" width="90" /></td>
        <td>
          <router-link
            :to="{ name: 'ProductEdit', params: { id: product.id } }"
            class="btn"
            >Edit</router-link
          >
          <button @click="del(product.id)" class="btn btn-del">Delete</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import { onMounted, ref } from 'vue'; 
export default {
  name: "Products",
  setup() {
    const products = ref([]);
    onMounted( async () => {
        const res = await fetch('httpls://localhost:3000/products');
        products.value = await res.json(); 
    });

    return {products}
  },
};
</script>

<style></style>
