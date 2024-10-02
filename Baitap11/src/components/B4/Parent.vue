<template>
  <div>
    <Children :age="age" />
    <p>Giá trị: {{ age }}</p>
    <button @click="handleIncrease">Increase</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Children from "./Children.vue";
const age = ref(0);

const handleIncrease = () => {
  age.value++;
};
</script>

<style></style>
