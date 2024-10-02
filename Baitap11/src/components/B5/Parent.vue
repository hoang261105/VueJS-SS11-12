<template>
  <div>
    <button @click="handleToggle">Toggle</button>
    <Children v-if="isOpen" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import Children from "../B5/Children.vue";
const isOpen = ref(false);
const handleToggle = () => {
  isOpen.value = !isOpen.value;
};
</script>

<style></style>
