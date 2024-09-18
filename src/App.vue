<script setup>
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
</script>

<template>
  <div class="app-container">
    <Header />
    <main class="main-content">
      <Form />
    </main>
  </div>
</template>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
}

.main-content {
  margin-top: 70px;
  padding: 20px;
}
</style>
