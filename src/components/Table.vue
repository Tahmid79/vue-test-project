<template>
  <v-data-table :items="items"></v-data-table>
</template>

<script setup lang="ts">
import { faker } from "@faker-js/faker";
import { onMounted, ref } from "vue";

let items = ref<any[]>([]);

onMounted(() => {
  // generateData(12);
});

function generateData(num: number) {
  const newItems: any = [];

  for (let i = 0; i < num; i++) {
    const item = {
      email: faker.internet.email(),
      potatoes: 12,
      fullName: faker.person.fullName(),
      location: faker.location.country(),
      tags: "Customer"
    };

    newItems.push(item);
  }

  items.value = newItems;
}

function sayHello() {
  console.log("hello");
}

defineExpose({
  sayHello,
  generateData
});
</script>

<style lang="scss"></style>
