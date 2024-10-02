<template>
  <div>
    <h1>Component Mounted</h1>
  </div>
</template>

<script setup>
import { onMounted } from "vue";

onMounted(() => {
  console.log("Component Mounted");
});
</script>

<style></style>
