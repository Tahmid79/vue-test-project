<template>
  <div>
    <v-app class="app-style">
      <v-main>
        <RouterView />
      </v-main>
    </v-app>
  </div>
</template>

<script setup lang="ts">
import { RouterView } from "vue-router";
</script>

<style scoped lang="scss">
.app-style {
  min-height: 100%;
  background-color: rgba(245, 245, 245, 1);
}
</style>
