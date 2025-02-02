<template>
  <v-container>
    <!-- Vuetify Data Table with Draggable Rows -->
    <v-data-table :items="items" item-key="fullName" class="elevation-1">
      <template>
        <draggable
          v-model="items"
          item-key="fullName"
          :group="{ name: 'items', pull: 'clone', put: true }"
          class="draggable-row"
        >
          <template #item="{ item }">
            <tr style="height: 30px; width: 100%" :key="item?.fullName">
              <td>{{ item?.fullName }}</td>
              <td>{{ item?.email }}</td>
              <td>{{ item?.location }}</td>
              <td>{{ item?.potatoes }}</td>
              <td>{{ item?.tags }}</td>
            </tr>
          </template>
        </draggable>
      </template>
    </v-data-table>
  </v-container>
</template>

<script setup lang="ts">
import { ref } from "vue";
import draggable from "vuedraggable"; // Import vuedraggable correctly

// Fake data for the items
const items = ref<any[]>([]);

// Define table headers
const headers = [
  { text: "Full Name", align: "start", key: "fullName" },
  { text: "Email", align: "start", key: "email" },
  { text: "Location", align: "start", key: "location" },
  { text: "Potatoes", align: "start", key: "potatoes" },
  { text: "Tags", align: "start", key: "tags" }
];

// Generate data for the table
const generateData = (num: number) => {
  const newItems: any[] = [];

  for (let i = 0; i < num; i++) {
    const item = {
      email: `example${i}@domain.com`,
      potatoes: 12,
      fullName: `Full Name ${i}`,
      location: `Location ${i}`,
      tags: "Customer"
    };

    newItems.push(item);
  }

  items.value = newItems;
};

// Generate 12 items for the list
generateData(12);

// For paginating the table
const itemsPerPage = ref(5);
</script>

<style scoped>
/* Style for draggable row */
.draggable-row {
  cursor: grab;
  transition: background-color 0.2s ease;
  background-color: #f9f9f9;
  border-radius: 4px;
  border: 1px solid #e0e0e0;
  padding: 10px;
}

.draggable-row:hover {
  background-color: #e0e0e0;
}

/* Add padding for table cells */
v-data-table td {
  padding: 10px 15px;
}
</style>
