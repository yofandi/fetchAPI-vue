<script setup>
import ProductCard from "@/components/ProductCard.vue";
import Pagination from "@/components/Pagination.vue";
import { onBeforeMount, onBeforeUpdate, onMounted, onUpdated, ref } from "vue";

const page = ref(1);

function nextPage() {
  page.value++;
}

onBeforeMount(() => {
  console.log("hai ini onBeforeMounted");
});

onMounted(() => {
  console.log("hai ini onMounted");
});

onBeforeUpdate(() => {
  console.log("Component akan segera tampil");
});

onUpdated(() => {
  console.log("Component sudah diperbaharui");
});
</script>

<template>
  <main>
    {{ page }}
    <button @click="nextPage">Next</button>
    <div class="product-grid">
      <ProductCard></ProductCard>
    </div>
    <div class="pagination">
      <Pagination></Pagination>
    </div>
  </main>
</template>

<style scoped>
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
