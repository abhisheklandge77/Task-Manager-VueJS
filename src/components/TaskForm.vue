<template>
  <div class="task-form-container">
    <div class="input-field">
      <input
        name="task-name"
        id="task-name"
        v-model="name"
        placeholder="Enter task name"
      />
    </div>
    <div class="date-time-field">
      <input
        name="task-date"
        v-model="date"
        id="task-date"
        type="date"
        placeholder="Enter date"
      />
      <input
        name="task-time"
        id="task-time"
        v-model="time"
        type="time"
        placeholder="Enter time"
      />
    </div>
    <div class="checkbox">
      <input name="reminder" v-model="reminder" id="reminder" type="checkbox" />
      <label for="reminder">Remind me</label>
    </div>

    <button class="save-task-btn" @click="saveTask()">Save Task</button>
  </div>
</template>

<script>
export default {
  name: "TaskForm",
  data() {
    return {
        name: "",
        reminder: false,
        date: "",
        time: "",
        months: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'], 
    };
  },
  methods: {
    saveTask() {
        if(!this.name){
            alert("Enter Task name first");
            return;
        }
        const date = this.date ? new Date(this.date) : new Date();
        const newDate = `${date.getDate()} ${this.months[date.getMonth()]} ${date.getFullYear()}`;
        const newTime = this.time ? this.time : `${date.getHours()}:${date.getMinutes()}`;
        const newTask = {
            id: Math.floor(Math.random() * 100000),
            name: this.name,
            date: newDate,
            time: newTime,
            reminder: this.reminder
        };

        this.$emit('save-task', newTask);

        this.name = "";
        this.reminder = false;
        this.date = "";
        this.time = "";
    },
  },
  emits: ['save-task']
};
</script>

<style scoped>
.task-form-container {
  color: #2c3e50;
  box-sizing: border-box;
  text-align: center;
  width: 40%;
  margin: 2rem auto;
}
.input-field {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}
.input-field input {
  outline: none;
  padding: 0.5rem;
  width: 100%;
}
.date-time-field {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}
.date-time-field input {
  outline: none;
  padding: 0.5rem;
  width: 42%;
}
.checkbox input {
  margin-right: 0.5rem;
  margin-bottom: 1rem;
}
.save-task-btn {
  border: none;
  outline: none;
  padding: 0.5rem;
  width: 100%;
  color: #fff;
  background-color: #2c3e50;
  cursor: pointer;
  border-radius: 5px;
  margin-top: 0.5rem;
}
</style>