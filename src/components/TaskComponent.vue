<template>
  <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'task-container reminder' : 'task-container']">
    <div class="task-text" title="Double click to set or unset reminder">
      <h3 class="task-name" v-bind:title="task.name" >{{ task.name }}</h3>
      <p>{{ `${task.date} at ${task.time}` }}</p>
    </div>
    <div class="delete-icon" @click="$emit('delete-task', task.id)">
    <i class="fa-solid fa-trash"></i>
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskComponent",
  props: {
    task: Object,
  },
  emits: ['delete-task', 'toggle-reminder']
};
</script>

<style scoped>
.task-container {
  background-color: #cfddec;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 5px;
  padding: 0.8rem;
  width: 70%;
  margin: 1.5rem auto;
}
.reminder{
    border-left: 5px solid #109230;
}
.task-text{
    width: 80%;
}
.task-name{
     overflow: hidden;
  text-overflow: ellipsis;
   white-space: nowrap;
}
.task-text h3,
p {

  margin: 0.2rem;
  color: #2c3e50;
}
.delete-icon {
  color: #2c3e50;
  margin-right: 0.5rem;
  cursor: pointer;
}
</style>