<template>
  <div>
    <h2>Ứng dụng đếm số</h2>
    <p>Count: {{ count }}</p>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from "vue";

const count = ref(0);
let intervalId = ref(null);

onMounted(() => {
  intervalId = setInterval(() => {
    count.value++;
  }, 1000);
});

onUnmounted(() => {
  clearInterval(intervalId.value);
});
</script>

<style></style>
