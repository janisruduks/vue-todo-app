<template>
  <v-container class="fill-height">
    <v-responsive class="align-center text-center fill-height">
      <v-row class="d-flex align-center justify-center">
        <v-col cols="auto">
          <submit-task :tasks="tasks" />
        </v-col>
      </v-row>
      <v-col>
        <v-app-bar-title class="pa-3">Active tasks</v-app-bar-title>
        <Tasks
          :tasks="activeTasks"
          @taskEvent="toggleTask"
          :fullTaskList="tasks"
        />
        <v-app-bar-title class="pa-3"> Completed tasks </v-app-bar-title>
        <Tasks
          :tasks="finishedTasks"
          @taskEvent="toggleTask"
          :fullTaskList="tasks"
        />
      </v-col>
    </v-responsive>
  </v-container>
</template>

<script lang="ts">
import SubmitTask from "./SubmitTask.vue";
import Tasks from "./Tasks.vue";
interface Task {
  src: string;
  title: string;
  text: string;
  active: boolean;
}
export default {
  data: () => ({
    tasks: [
      {
        title: "Buy Cat Food",
        src: "https://i.pinimg.com/originals/fc/c5/31/fcc531c29bed3fd4b1f6eefff6622918.gif",
        text: "Don't forget to buy your cat's favorite food!",
        active: true,
      },
      {
        title: "Schedule Vet Appointment",
        src: "https://media1.giphy.com/media/9VgopxrAp27xH6vS6S/giphy.gif?cid=6c09b952g31iadyhc9wgsdukfvbsfam04wyndson1rrepswe&ep=v1_internal_gif_by_id&rid=giphy.gif&ct=s",
        text: "It's time for your cat's annual checkup. Call the vet to schedule an appointment.",
        active: false,
      },
      {
        title: "Playtime with Kitty",
        src: "https://usagif.com/wp-content/uploads/gifs/happy-cat-26.gif",
        text: "Spend quality playtime with your cat. Use their favorite toys and make them happy!",
        active: false,
      },
    ],
  }),
  watch: {
    tasks: {
      handler(newTasks) {
        localStorage.setItem("tasks", JSON.stringify(newTasks));
      },
      deep: true,
    },
  },

  created() {
    const storedTasks = localStorage.getItem("tasks");
    if (storedTasks) {
      this.tasks = JSON.parse(storedTasks);
    }
  },
  methods: {
    toggleTask(task: Task) {
      task.active = !task.active;
    },
    updateTaskList(updatedTaskList: Task[]) {
      this.tasks = updatedTaskList;
    },
  },
  computed: {
    activeTasks(): Task[] {
      return this.tasks.filter((task) => task.active);
    },
    finishedTasks(): Task[] {
      return this.tasks.filter((task) => !task.active);
    },
  },
  components: { SubmitTask, Tasks },
};
</script>
