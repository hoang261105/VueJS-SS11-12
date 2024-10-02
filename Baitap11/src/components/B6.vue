<template>
  <div>
    <p>{{ count }}</p>
    <button @click="handleIncrease">Increment</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const count = ref(0);
const handleIncrease = () => {
  count.value += 1;
  document.title = count.value;
};
</script>

<style></style>
