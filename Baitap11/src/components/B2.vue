<template>
  <div>
    <p>Giá trị count: {{ count }}</p>
    <button @click="handleIncrease">Counter</button>
  </div>
</template>

<script setup>
import { onUpdated, ref } from "vue";

const count = ref(0);
const handleIncrease = () => {
  count.value += 1;
};
onUpdated(() => console.log("Dữ liệu đã thay đổi"));
</script>

<style></style>
