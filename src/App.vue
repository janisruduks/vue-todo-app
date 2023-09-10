<template>
  <v-app>
    <v-main class="bg">
      <v-app-bar :elevation="3">
        <v-app-bar-title>My tasks app</v-app-bar-title>
        <v-app-bar-nav-icon icon="mdi-circle"></v-app-bar-nav-icon>
      </v-app-bar>
      <TaskSection />
      <v-footer>
      <div class="text-center w-100">
        2023 — <strong>Task App</strong>
      </div>
      </v-footer>
    </v-main>
  </v-app>
</template>

<style>
.bg {
  background-color: #f5f5f5;
}
</style>

<script setup lang="ts">
import TaskSection from "@/components/TaskSection.vue";
</script>
