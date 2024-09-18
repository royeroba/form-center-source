<template>
  <div class="card">
    <h3 class="title">User data</h3>
    <p><strong>Name:</strong> {{ formData.name }}</p>
    <p><strong>Email:</strong> {{ formData.email }}</p>
    <p><strong>Phone:</strong> {{ formData.phone }}</p>
    <p v-if="formData.otherPhone">
      <strong>Other Phone:</strong> {{ formData.otherPhone }}
    </p>
  </div>
</template>

<script setup>
const props = defineProps({
  formData: {
    type: Object,
    required: true,
  },
});
</script>

<style scoped>
.card {
  background-color: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
  margin-top: 20px;
}

.title {
  display: flex;
  color: #ffa500;
  justify-content: center;
  align-items: center;
}

h3 {
  margin-bottom: 20px;
}

p {
  margin: 5px 0;
  font-size: 16px;
}
</style>
