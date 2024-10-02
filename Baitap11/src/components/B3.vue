<template>
  <div>
    <p>Current Company: {{ currentCompany }}</p>
    <p>Age: {{ age }}</p>
    <button @click="handleRandom">Random</button>
  </div>
</template>

<script setup>
import { computed, onUpdated, reactive, ref } from "vue";

const age = ref(1);
const companies = reactive([
  "Rikkei Academy",
  "Rikkei Education",
  "Rikkei Fukuoka",
]);

const handleRandom = () => {
  age.value = Math.ceil(Math.random() * 10);
};

const currentCompany = computed(() => {
  return companies[(age.value - 1) % companies.length];
});
</script>

<style></style>
