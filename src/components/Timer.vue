<template>
  <div class="countdown-container">
    <p class="countdown-text">{{ countDownText }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const countDownText = ref("");
const countDownDuration = 0.2 * 60 * 1000; // 5 minutes in milliseconds
const endTime = new Date().getTime() + countDownDuration;

const updateCountdown = () => {
  const now = new Date().getTime();
  const distance = endTime - now;

  const minutes = Math.floor(distance / (1000 * 60));
  const seconds = Math.floor((distance % (1000 * 60)) / 1000);

  countDownText.value = `${minutes}m ${seconds}s`;

  if (distance <= 0) {
    clearInterval(timer);
    countDownText.value = "EXPIRED";
  }
};

const timer = setInterval(updateCountdown, 1000);
</script>

<style lang="scss" scoped>
.countdown-container {
  width: 90%;
  display: flex;
  justify-content: center;
}

.countdown-text {
  font-weight: bold;
  font-size: 24px;
}
</style>
