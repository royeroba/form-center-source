<template>
  <header class="header">
    <div class="logo">
      <img src="../assets/img/logo.png" alt="Logo" />
    </div>
  </header>
</template>

<script setup></script>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  width: 100%;
  background-color: white;
  padding: 10px 20px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
}

.logo img {
  width: 100%;
  height: 4rem;
}
</style>
