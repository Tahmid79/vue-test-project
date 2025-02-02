<template>
  <div>
    <div class="top-segment">
      <h1 class="title">Sorting Training System</h1>
      <DialogTest @number-event="handleNumberEvent" />
    </div>
  </div>

  <div>
    <DragTest ref="tableRef" />
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, nextTick } from "vue";
import DialogTest from "../components/DialogTest.vue";
import DragTest from "../components/DragTest.vue";

const tableRef = ref<typeof Table | null>(null); // Type the ref as Table or null

function handleNumberEvent(event: any) {
  const num: number = event;
  console.log(num);

  if (tableRef?.value) {
    tableRef?.value?.generateData(num); // Call the method only if it's available
  }
}

// onMounted(() => {
//   nextTick(() => {
//     if (tableRef?.value) {
//       tableRef?.value?.sayHello(); // Call the method only if it's available
//     }
//   });
// });
</script>

<style lang="scss" scoped>
.top-segment {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center; /* Align items along the cross axis */
  margin: 12px 16px;
  height: 60px;
}

.title {
  font-size: 32px;
  margin: 0;
}

:deep(.v-toolbar-title) {
  font-weight: bold;
}
</style>
