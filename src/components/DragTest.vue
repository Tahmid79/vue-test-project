<template>
  
  <table class="draggable-container empty-table" v-if="items?.length === 0">    
    <tbody>
      <tr>
        <td align="center">
          <h1 class="mx-32 empty-text">No data available</h1>
        </td>
      </tr>
    </tbody>
  </table>
  
  <div class="timer-height">
    <Timer ref="timerComponentRef" v-if="items?.length > 0" />
  </div>
  
  <div v-if="showSuccess" class="success-segment my-4">
    <div class="success-inner-segment">
      <h1 class="success-text" >Success!</h1>
      <p class="success-subtitle">Your score is 100</p>
    </div>
    
  </div>
  
  <table v-if="items?.length > 0" class="draggable-container">
    <thead class="header-container">
      <tr class="table-top-segment" style="display: flex; justify-content: end">
        <p class="list-text">{{ items?.length }} people in the list</p>
      </tr>
      <tr>
        <td class="no-right-border">
          <th width="40%" class="column-header cell-size">Email</th>
          <th width="10%" class="column-header cell-size">Potatoes</th>
          <th width="10%" class="column-header cell-size">Tags</th>
          <th width="20%" class="column-header cell-size">Name</th>
          <th width="20%" class="column-header cell-size">Location</th>
        </td>
      </tr>
    </thead>
    
    <tbody>
      <draggable
        v-model="items"
        item-key="fullName"
        @start="dragStart"
        @end="dragEnd"
        :group="{ name: 'items', pull: 'clone', put: true }"
      >
        <template style="width: 100%" #item="{ element }">
          <tr
            class="draggable-item item-content"
            :class="{ 'checked-hover-color': element.checked }"
          >
            <td width="40%">
              <input
                class="custom-checkbox"
                type="checkbox"
                id="email-checkbox"
                name="vehicle1"
                :value="element.checked"
                @click="element.checked = !element.checked"
              />
              <span class="email-text">{{ element.email }}</span>              
            </td>
            <td class="cell-size" width="10%">{{ element.potatoes }}</td>
            <td class="cell-size" width="10%">
              <div class="customer-tag">
                <p class="customer-text">{{ element.tags }}</p>
              </div>
            </td>
            <td class="cell-size" width="20%">{{ element.fullName }}</td>
            <td class="cell-size" width="20%">{{ element.location }}</td>
          </tr>
        </template>
      </draggable>
    </tbody>
  </table>
</template>

<script setup lang="ts">
import { faker } from "@faker-js/faker";
import { ref } from "vue";
import draggable from "vuedraggable";
import Timer from "./Timer.vue";

const items = ref<any[]>([]);
const ex4 = ref();
const showSuccess = ref(false);
let timerComponentRef = ref<typeof Timer | null>(null);

const isSortedByPotatoesDescending = (arr: any[]): boolean => {
  if (!arr) return false;
  if (arr.length <= 1) return true;

  for (let i = 1; i < arr.length; i++) {
    if (arr[i].potatoes > arr[i - 1].potatoes) {
      return false;
    }
  }
  return true;
};


function shuffle(array: any[]) {
  let currentIndex = array.length;

  // While there remain elements to shuffle...
  while (currentIndex != 0) {

    // Pick a remaining element...
    let randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex--;

    // And swap it with the current element.
    [array[currentIndex], array[randomIndex]] = [
      array[randomIndex], array[currentIndex]];
  }
}

const generateData = (num: number) => {
  if(timerComponentRef?.value){
    timerComponentRef?.value?.resetTimer();
  }

  const newItems: any[] = [];

  let potatoesCount = 1;

  for (let i = 0; i < num; i++) {
    const item = {
      email: faker.internet.email(),
      potatoes: potatoesCount,
      fullName: faker.person.fullName(),
      location: faker.location.country(),
      tags: "Customers",
      checked: false
    };

    potatoesCount += 1;

    newItems.push(item);
  }
  shuffle(newItems);
  items.value = newItems;
};

// Generate 12 items for the list
// generateData(12);

const dragStart = () => {
  console.log("Drag started");
};

const dragEnd = () => {
  // console.log(items.value);
  const isSorted = isSortedByPotatoesDescending(items.value);
  if(isSorted){
    // alert('Success');
    showSuccess.value = true;
    setTimeout(()=> {
      showSuccess.value = false;
      items.value = [];
      if(timerComponentRef?.value){
        timerComponentRef?.value?.stopTimer();
      }
    }, 2000);
  }
  console.log("Drag ended");
};

defineExpose({
  generateData
});
</script>

<style scoped lang="scss">
.table-top-segment {
  border-bottom: 1px solid #ddd;
  padding: 12px;
  padding-right: 16px;
}

.list-text {
  font-weight: bold;
}

.draggable-container {
  // width: 90%;
  margin: 20px auto;
  border-collapse: collapse;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
  overflow: hidden;
  background-color: white;
  /* table-layout: auto; */
}

.column-header {
  // width: auto;
  // width: 20%;
  // height: 48px;
  border-bottom: none;
  font-family: Roboto;
  font-size: 14px;
  font-weight: 400;
  line-height: 18px;
  text-align: left;
  text-underline-position: from-font;
  text-decoration-skip-ink: none;
  color: rgba(85, 85, 85, 1);
}

th,
td {  
  text-align: left;
  border-bottom: 1px solid #ddd;
  word-wrap: break-word;
  overflow-wrap: break-word;
}

td:first-child {
  border-right: 1px solid #ddd;
}

th {
  // background-color: #f3f3f3;
  font-weight: bold;
}

tr:hover {
  background-color: #f9f9f9;
}

.checked-hover-color {
  background-color: rgba(245, 245, 245, 1) !important;
}

.draggable-item {
  transition: background-color 0.2s;
  cursor: move;
  display: table-row;
  width: 100%;
  table-layout: auto;
}

.draggable-item:hover {
  background-color: #e6f7ff;
}

.item-content td {
  // padding: 10px 15px;
  font-size: 0.95rem;
}

.item-content td:first-child {
  font-weight: 600;
}

.cell-size{
  height: 32px;
  padding: 8px;
}

.email-text{
  font-family: Roboto;
  font-size: 14px;
  font-weight: 400;
  line-height: 18px;
  text-align: left;
  text-underline-position: from-font;
  text-decoration-skip-ink: none;
  color: rgba(0, 0, 0, 1);
  margin-left: 8px;
}

#email-checkbox{  
}

.customer-tag{
  width: 84px;
  height: 28px;
  gap: 0px;
  border-radius: 16px;
  opacity: 0px;
  background: rgba(238, 238, 238, 1);
  display: flex;
}

.customer-text{
    font-family: Roboto;
    font-size: 13px;
    font-weight: 400;
    line-height: 16px;
    text-align: center;
    text-underline-position: from-font;
    text-decoration-skip-ink: none;
    color: rgba(85, 85, 85, 1);
    margin: auto;
    width: 100%;
}

.empty-table{
  width: 90%;
  height: 200px;
}

.empty-text{
  text-align: center;
}

.timer-height{
  height: 40px;
  margin-bottom: 20px;
}

.no-right-border{
  border-right: 0px !important;
}

.success-segment{
  width: 100%;
  background-color: lightgreen;
  height: 120px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 6px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.success-inner-segment{

}

.success-text{
  color: white;
  margin: 0;
  padding: 0;
}

.success-subtitle{
  color: white;
  margin: 0;
  padding: 0;
}

// Checkbox Styling

.custom-checkbox {
  appearance: none;
  width: 16px;
  height: 16px;
  border: 2px solid #ddd;
  border-radius: 4px;
  cursor: pointer;
  position: relative;
  display: inline-block;
  background-color: white;
  vertical-align: middle;
}

.custom-checkbox:checked {
  background-color: orange;
  border-color: orange;
}

.custom-checkbox:checked::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 5px;
  height: 9px;
  border: solid white;
  border-width: 0 2px 2px 0;
  transform: translate(-50%, -50%) rotate(45deg);
}

/* Responsive Design */
@media screen and (max-width: 768px) {
  .draggable-container {
    width: 100%;
  }

  // th,
  // td {
  //   padding: 10px;
  // }
}
</style>
