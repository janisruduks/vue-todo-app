<template>
  <v-card max-width="600" class="mx-auto">
    <v-container>
      <v-item-group multiple>
        <v-row>
          <v-col v-for="(task, i) in tasks" :key="i" cols="12" md="4">
            <v-item>
              <v-img
                :src="`${task.src}`"
                cover
                height="100"
                class="text-right pa-2"
              >
                <v-btn
                  size="32"
                  :icon="task.active ? 'mdi-close' : 'mdi-check'"
                  :color="task.active ? 'red' : 'green'"
                  @click="toggleSelection(task)"
                />
                <v-btn icon="mdi-delete" size="32" @click="deleteTask(task)" />
              </v-img>
              <v-card-title
                :style="task.active ? '' : 'text-decoration: line-through;'"
              >
                {{ task.title }}
              </v-card-title>
              <v-card-text
                :style="task.active ? '' : 'text-decoration: line-through;'"
              >
                {{ task.text }}
              </v-card-text>
            </v-item>
          </v-col>
        </v-row>
      </v-item-group>
    </v-container>
  </v-card>
</template>

<script lang="ts">
import { PropType } from "vue";
import { defineComponent } from "vue";
interface Task {
  src: string;
  title: string;
  text: string;
  active: boolean;
}
export default defineComponent({
  props: {
    tasks: {
      type: Array as PropType<Task[]>,
      required: true,
    },
    fullTaskList: {
      type: Array as PropType<Task[]>,
      required: true,
    },
  },
  methods: {
    deleteTask(taskToDelete: Task) {
      const updatedFullTaskList = this.fullTaskList.filter(
        (task) => task !== taskToDelete
      );

      this.$emit("update:fullTaskList", updatedFullTaskList);
    },
  },
  setup(props, { emit }) {
    const toggleSelection = (task: Task) => {
      emit("taskEvent", task);
    };
    const deleteTask = (task: Task) => {
      const index = props.fullTaskList.indexOf(task);
      if (index !== -1) {
        props.fullTaskList.splice(index, 1);
      }
      emit("update:fullTaskList", props.fullTaskList.slice());
    };

    return {
      toggleSelection,
      deleteTask,
    };
  },
});
</script>
