<template>
  <input type="text" v-model="inputValue" @input="handleChange" />
</template>

<script setup>
import { ref } from "vue";

const inputValue = ref("");
const handleChange = () => {
  document.title = inputValue.value;
};
</script>

<style></style>
