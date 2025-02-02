<template>
  <div>
    <v-app-bar class="d-flex justify-space-between">
      <v-app-bar-title class="mx-5">Sorting Training System</v-app-bar-title>
      <!-- <v-btn> Button </v-btn> -->
      <DialogTest @number-event="handleNumberEvent" />
    </v-app-bar>
  </div>

  <div>
    <!-- <DialogTest @number-event="handleNumberEvent" /> -->

    <!-- <Table ref="tableRef" /> -->

    <DragTest ref="tableRef" />
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, nextTick } from "vue";
import DialogTest from "../components/DialogTest.vue";
import Table from "../components/Table.vue";
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
:deep(.v-toolbar-title) {
  font-weight: bold;
}
</style>
