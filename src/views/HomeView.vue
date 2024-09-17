<script setup>
import ProductCard from "@/components/ProductCard.vue";
import Pagination from "@/components/Pagination.vue";
import Loading from "@/components/Loading.vue";

import { onMounted, ref, watch, watchEffect } from "vue";
import axios from "axios";

const isLoading = ref(true);
const products = ref([]);
const page = ref(1);
const limit = ref(8);

async function fetchData() {
  const API_URL = `http://localhost:3000/products?_page=${page.value}&_per_page=${limit.value}`;
  try {
    isLoading.value = true;
    const response = await axios.get(API_URL);
    products.value = response.data;
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(() => {
      isLoading.value = false; // Stop loading after 2 seconds
    }, 500);
  }
}

// onMounted(async () => {
//   try {
//     products.value = await axios.get(API_URL).then((res) => res.data);
//     console.log(products.value);
//   } catch (error) {
//     console.log(error);
//   } finally {
//     setTimeout(() => {
//       isLoading.value = false; // Stop loading after 2 seconds
//     }, 500);
//   }
// });

// watch(page, async () => {
//   try {
//     isLoading.value = true;
//     products.value = await axios.get(API_URL).then((res) => res.data);
//     console.log(products.value);
//   } catch (error) {
//     console.log(error);
//   } finally {
//     setTimeout(() => {
//       isLoading.value = false; // Stop loading after 2 seconds
//     }, 500);
//   }
// });
watchEffect(() => {
  fetchData();
});

function changePage(newPage) {
  if (newPage < 1) return;
  if (newPage > products.value.pages) return;
  page.value = newPage;
}
// async function getProducts() {
//   const response = await axios.get("http://localhost:3000/products");
//   products.value = response.data;
//   console.log(response.data);
// }

// getProducts();
</script>

<template>
  <!-- Loading Screen -->
  <div v-if="isLoading" class="loading-screen">
    <Loading></Loading>
  </div>
  <main v-else>
    <div class="product-grid">
      <ProductCard
        v-for="(product, index) in products.data"
        :key="index"
        :product="product"
      ></ProductCard>
    </div>
    <div class="pagination">
      <Pagination
        :page="page"
        :totalPages="products.pages"
        @change-page="changePage"
      ></Pagination>
    </div>
  </main>
</template>

<style scoped>
.loading-screen {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  flex-direction: column;
  background-color: #f5f5f5;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
  width: 80%;
  margin: 0 auto;
}
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}
</style>
