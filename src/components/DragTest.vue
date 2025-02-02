<template>
  <table class="draggable-container">
    <tbody>
      <tr>
        <th>Email</th>
        <th>Potatoes</th>
        <th>Tags</th>
        <th>Name</th>
        <th>Location</th>
      </tr>

      <draggable
        v-model="items"
        item-key="fullName"
        @start="dragStart"
        @end="dragEnd"
        :group="{ name: 'items', pull: 'clone', put: true }"
      >
        <template #item="{ element }">
          <tr class="draggable-item item-content">
            <!-- <td>Email: {{ element.email }}</td>
            <td>Potatoes: {{ element.potatoes }}</td>
            <td>Tags: {{ element.tags }}</td>
            <td>Name: {{ element.fullName }}</td>            
            <td>Location: {{ element.location }}</td> -->

            <td>{{ element.email }}</td>
            <td>{{ element.potatoes }}</td>
            <td>{{ element.tags }}</td>
            <td>{{ element.fullName }}</td>
            <td>{{ element.location }}</td>
          </tr>
        </template>
      </draggable>
    </tbody>
  </table>
</template>

<script setup lang="ts">
import { faker } from "@faker-js/faker";
import { ref } from "vue";
import draggable from "vuedraggable"; // Import vuedraggable correctly

// Fake data for the items
const items = ref<any[]>([]);

const generateData = (num: number) => {
  const newItems: any[] = [];

  let potatoesCount = 1;

  for (let i = 0; i < num; i++) {
    const item = {
      email: faker.internet.email(),
      potatoes: potatoesCount,
      fullName: faker.person.fullName(),
      location: faker.location.country(),
      tags: "Customer"
    };

    potatoesCount += 1;

    newItems.push(item);
  }

  items.value = newItems;
};

// Generate 12 items for the list
generateData(12);

// Start and end drag events
const dragStart = () => {
  console.log("Drag started");
};

const dragEnd = () => {
  console.log("Drag ended");
};

defineExpose({
  generateData
});
</script>

<style scoped>
.draggable-container {
  width: 80%;
  margin: 0 auto;
}

.draggable-item {
  padding: 15px;
  margin: 10px 0;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
  transition: background-color 0.2s ease;
  cursor: grab; /* Add cursor style to indicate the item is draggable */
}

.draggable-item:active {
  cursor: grabbing; /* Add grabbing cursor when dragging */
}

.draggable-item:hover {
  background-color: #e0e0e0;
}

.item-content h3 {
  font-size: 1.2rem;
  font-weight: bold;
}

.item-content p {
  margin: 5px 0;
  font-size: 0.9rem;
}

table {
  border: 1px solid #dddddd;
  border-radius: 4px;
  box-shadow: 0px 0px 4px 0px rgba(0, 0, 0, 0.102);
}

td {
  width: 20%;
}

tr {
  border: 1px solid black;
  height: 48px;
  width: 100%;
}
</style>
