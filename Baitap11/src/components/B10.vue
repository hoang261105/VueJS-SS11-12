<template>
  <div class="clock">Thời gian hiện tại: {{ time }}</div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

// Biến để lưu trữ thời gian
const time = ref("");

// Hàm để cập nhật thời gian thực
const updateTime = () => {
  const now = new Date();
  const hours = String(now.getHours()).padStart(2, "0");
  const minutes = String(now.getMinutes()).padStart(2, "0");
  const seconds = String(now.getSeconds()).padStart(2, "0");
  time.value = `${hours} : ${minutes} : ${seconds}`;
};

let intervalId;

// Khi component được mount, cập nhật thời gian mỗi giây
onMounted(() => {
  updateTime(); // Cập nhật lần đầu tiên ngay khi mounted
  intervalId = setInterval(updateTime, 1000);
});

// Dọn dẹp bộ nhớ khi component bị hủy
onUnmounted(() => {
  clearInterval(intervalId);
});
</script>

<style scoped>
.clock {
  font-size: 24px;
  font-weight: bold;
}
</style>
