<template>
  <div class="todo-container">
    <TaskHeader title="Task Manager" :showCreateTaskBtn="showTaskForm" @show-task-form="createTask" />

    <div v-show="showTaskForm">
    <TaskForm @save-task="saveTask"/>
    </div>

    <div :key="task.id" v-for="task in tasks">
      <TaskComponent
        :task="task"
        @delete-task="deleteTask(task.id)"
        @toggle-reminder="toggleReminder(task.id)"
      />
    </div>
  </div>
</template>

<script>
import TaskHeader from "./components/TaskHeader.vue";
import TaskForm from "./components/TaskForm.vue";
import TaskComponent from "./components/TaskComponent.vue";

export default {
  name: "App",
  components: {
    TaskHeader,
    TaskForm,
    TaskComponent,
  },
  data() {
    return {
      tasks: [],
      showTaskForm: false,
    };
  },
  methods: {
    createTask() {
      this.showTaskForm = !this.showTaskForm;
    },

    saveTask(newTask) {
      this.tasks = [...this.tasks, newTask];
    },

    deleteTask(id) {
      const task = this.tasks.find((task) => task.id === id);
      if (confirm(`Are you sure you want to delete ${task.name} ?`)) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },

    toggleReminder(id) {
      this.tasks = this.tasks.map(task => 
        task.id === id ? 
        {...task, reminder: !task.reminder} : 
        task
      )
    },
  },
  created() {
    this.tasks = [];
    this.showTaskForm = !this.tasks.length ? true : false;
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.todo-container {
  border: 1px solid #2c3e50;
  width: 60%;
  margin: 0 auto;
}
</style>