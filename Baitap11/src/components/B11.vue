<template>
  <div class="traffic-light">
    <div :class="['light', currentLight === 'red' ? 'active-red' : '']"></div>
    <div
      :class="['light', currentLight === 'yellow' ? 'active-yellow' : '']"
    ></div>
    <div
      :class="['light', currentLight === 'green' ? 'active-green' : '']"
    ></div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

// Đèn giao thông gồm 3 màu: đỏ, vàng, xanh
const lights = ["red", "yellow", "green"];
const currentLight = ref("red"); // Mặc định bắt đầu với đèn đỏ
let intervalId;

// Hàm chuyển đổi đèn giao thông
const changeLight = () => {
  if (currentLight.value === "red") {
    currentLight.value = "green";
    setTimeout(() => {
      changeLight(); // Chuyển sang đèn xanh trong 60s
    }, 60000);
  } else if (currentLight.value === "green") {
    currentLight.value = "yellow";
    setTimeout(() => {
      changeLight(); // Chuyển sang đèn vàng trong 3s
    }, 3000);
  } else if (currentLight.value === "yellow") {
    currentLight.value = "red";
    setTimeout(() => {
      changeLight(); // Chuyển sang đèn đỏ trong 40s
    }, 40000);
  }
};

// Bắt đầu chu trình khi component được mount
onMounted(() => {
  changeLight();
});

// Dọn dẹp bộ nhớ khi component bị hủy
onUnmounted(() => {
  clearTimeout(intervalId);
});
</script>

<style scoped>
.traffic-light {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 60px;
  padding: 20px;
  background-color: #333;
  border-radius: 10px;
}

.light {
  width: 40px;
  height: 40px;
  margin: 10px 0;
  border-radius: 50%;
  background-color: gray;
  transition: background-color 0.3s ease;
}

.active-red {
  background-color: red;
}

.active-yellow {
  background-color: yellow;
}

.active-green {
  background-color: green;
}
</style>
