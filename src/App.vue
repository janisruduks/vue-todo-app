<template>
  <v-app>
    <v-main>
      <v-app-bar :elevation="3">
        <v-app-bar-title><v-btn href="/">My tasks app</v-btn></v-app-bar-title>
        <ThemeSwitcherButton />
        <v-app-bar-nav-icon icon="mdi-circle" />
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

<script setup lang="ts">
import TaskSection from "@/components/TaskSection.vue";
import ThemeSwitcherButton from "./components/ThemeSwitcherButton.vue";
</script>
