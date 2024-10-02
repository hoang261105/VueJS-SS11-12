<template>
  <div>
    <p>1234567890</p>
  </div>
</template>

<script setup>
import { onBeforeUnmount, onUnmounted } from "vue";

onBeforeUnmount(() => {
  console.log("Component is about to be unmounted");
});
onUnmounted(() => {
  console.log("Component is unmounted");
});
</script>

<style></style>
