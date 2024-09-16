<script setup></script>

<template>
  <div class="spinner"></div>
  <p>Loading...</p>
</template>

<style scoped>
/* Simple loading spinner */
.spinner {
  border: 4px solid rgba(0, 0, 0, 0.1);
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border-left-color: #3498db;
  animation: spin 1s ease infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

p {
  margin-top: 10px;
  font-size: 18px;
  color: #3498db;
}
</style>
