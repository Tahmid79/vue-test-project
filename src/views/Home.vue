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

const tableRef = ref<typeof DragTest | null>(null);

function handleNumberEvent(event: any) {
  const num: number = event;
  console.log(num);
  if (tableRef?.value) {
    tableRef?.value?.generateData(num);
  }
}
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

@media only screen and (max-width: 600px) {
  .top-segment {
    display: flex;
    flex-direction: column;
    height: fit-content;
    h1 {
      line-height: 1.2em;
      margin-top: 12px;
      margin-bottom: 12px;
    }
  }
}
</style>
