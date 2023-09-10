<template>
  <v-sheet width="600" min-width="300">
    <v-expansion-panels>
      <v-expansion-panel>
        <v-expansion-panel-title>
          <v-row no-gutters>
            <v-col cols="12" class="d-flex justify-start align-center">
              <v-icon icon="mdi-heart" size="large" start />
              Add task
            </v-col>
          </v-row>
        </v-expansion-panel-title>

        <v-expansion-panel-text>
          <v-text-field
            hide-details
            placeholder="Task name"
            v-model="newTaskName"
          >
          </v-text-field>
          <v-text-field
            hide-details
            placeholder="Task description"
            v-model="newTaskDescription"
          >
          </v-text-field>
          <v-text-field
            hide-details
            placeholder="Image url"
            v-model="newTaskImageUrl"
          >
          </v-text-field>
          <v-btn type="submit" block class="mt-2" @click="addItem"
            >Submit</v-btn
          >
        </v-expansion-panel-text>
      </v-expansion-panel>
    </v-expansion-panels>
  </v-sheet>
</template>

<script lang="ts">
export default {
    props: {
        tasks: Array,
    },
  data: () => ({
    newTaskName: "",
    newTaskDescription: "",
    newTaskImageUrl: "",
    active: true,
  }),

  methods: {
    addItem() {
      const newItem = {
        src: this.newTaskImageUrl,
        text: this.newTaskDescription,
        title: this.newTaskName,
        active: this.active,
      };
      this.tasks?.push(newItem);

      this.newTaskName = "";
      this.newTaskDescription = "";
      this.newTaskImageUrl = "";
    },
  },
};
</script>