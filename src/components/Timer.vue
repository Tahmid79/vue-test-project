<template>
  <div class="countdown-container">
    <p class="countdown-text">{{ countDownText }}</p>
    <!-- <v-btn @click="resetTimer">Reset Timer</v-btn>
    Button to reset the timer
    <v-btn @click="stopTimer">Stop Timer</v-btn>
    Button to stop the timer -->
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const countDownText = ref("0m 0s"); // Start from 0
let startTime = new Date().getTime(); // Start from the current time
let elapsedTime = 0;

let timer: ReturnType<typeof setInterval>; // Declare the timer variable

const updateCountdown = () => {
  const now = new Date().getTime();
  elapsedTime = now - startTime; // Calculate elapsed time

  const hours = Math.floor(elapsedTime / (1000 * 60 * 60)); // Convert elapsed time to hours
  const minutes = Math.floor((elapsedTime % (1000 * 60 * 60)) / (1000 * 60)); // Convert remaining time to minutes
  const seconds = Math.floor((elapsedTime % (1000 * 60)) / 1000); // Convert remaining time to seconds

  // Conditionally format the text to include hours only if greater than 0
  if (hours > 0) {
    countDownText.value = `${hours}h ${minutes}m ${seconds}s`;
  } else {
    countDownText.value = `${minutes}m ${seconds}s`;
  }
};

const startTimer = () => {
  // Start the countdown
  timer = setInterval(updateCountdown, 1000);
};

const resetTimer = () => {
  startTime = new Date().getTime(); // Reset the start time to the current time
  elapsedTime = 0; // Reset elapsed time
  countDownText.value = "0m 0s"; // Reset display text
  startTimer(); // Restart the timer
};

const stopTimer = () => {
  clearInterval(timer); // Stop the timer
};

startTimer(); // Start the timer when the page loads

defineExpose({
  startTimer,
  resetTimer,
  stopTimer
});
</script>

<style lang="scss" scoped>
.countdown-container {
  width: 90%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.countdown-text {
  font-weight: bold;
  font-size: 24px;
}

.v-btn {
  margin-top: 20px;
}
</style>
