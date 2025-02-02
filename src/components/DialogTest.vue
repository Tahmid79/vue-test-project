<template>
  <div class="pa-4 text-center">
    <v-dialog v-model="dialog" max-width="600">
      <template v-slot:activator="{ props: activatorProps }">
        <v-btn
          class="sorting-button"
          text="Start sorting!"
          variant="plain"
          v-bind="activatorProps"
        ></v-btn>
      </template>

      <v-card title="How many people">
        <hr class="divider-modal" />
        <v-card-text>
          <v-row dense>
            <v-col cols="12" md="12" sm="6">
              <p class="number-label">
                Enter a number of how many people you want to see in the list
              </p>
              <v-text-field
                class="number-input"
                v-model="numPeople"
                required
                variant="outlined"
              ></v-text-field>
            </v-col>

            <!-- <v-col cols="12" md="4" sm="6">
              <h1>{{ numPeople }}</h1>
            </v-col> -->
          </v-row>

          <!-- <small class="text-caption text-medium-emphasis"
            >*indicates required field</small
          > -->
        </v-card-text>

        <hr class="divider-modal" />

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn
            text="Cancel"
            class="cancel-button"
            variant="plain"
            @click="dialog = false"
          >
          </v-btn>

          <v-btn
            class="save-button"
            color="primary"
            text="Start"
            variant="plain"
            @click="saveNumber()"
          ></v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

let numPeople = ref<any>();
let dialog = ref<any>();

const emit = defineEmits(["number-event"]);

function saveNumber() {
  dialog.value = false;
  console.log(numPeople.value);
  const num: number = +numPeople.value;
  emit("number-event", num);
}

// export default {
//   data: () => ({
//     dialog: false
//   })
// };
</script>

<style lang="scss" scoped>
.number-label {
  color: #555555;
}

.number-input {
  padding: 0;
}

.divider-modal {
  border: 1px solid lightgray;
  width: 100%;
}

:deep(.v-field__field input) {
  padding-top: 0 !important;
  padding-bottom: 0 !important;
}

:deep(.v-card-title) {
  font-weight: bold;
}

.cancel-button {
  width: 88px;
  height: 40px;
  border-radius: 5px;

  background-color: #eeeeee;
  color: #555555;
  opacity: 1;
  font-weight: bold;
  font-size: 12px;
}

.save-button {
  width: 88px;
  height: 40px;
  border-radius: 5px;

  background-color: #ff8d00;
  color: white !important;
  opacity: 1;
  font-weight: bold;
  font-size: 12px;
  opacity: 1;
}

// button style

.sorting-button {
  background-color: rgba(255, 141, 0, 1);
  height: 54px;
  border-radius: 5px;
  color: white;
  font-size: 15px;
  margin-right: 24px;
  opacity: 1;
}
</style>
