<template>
  <div></div>
</template>

<script setup>
import { onUpdated } from "vue";

const age = defineProps({
  age: {
    type: Number,
    required: true,
  },
});
onUpdated(() => {
  alert("Giá trị của biến thay đổi");
});
</script>

<style></style>
