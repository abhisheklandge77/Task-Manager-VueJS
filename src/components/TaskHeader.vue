<template>
    <div class="header-container">
        <h2 class="title">{{title}}</h2>
        <button @click="this.$emit('show-task-form')" :class="[!showCreateTaskBtn ? 'create-task-btn': 'close-btn']">{{!showCreateTaskBtn ? "Create Task" : "Close"}}</button>
    </div>
</template>

<script>
export default {
    name: "TaskHeader",
    props: {
        title: String,
        showCreateTaskBtn: Boolean,
    },
    emits: ['show-task-form']
}
</script>

<style scoped>
.header-container{
    color: #2c3e50;
    display: flex;
    justify-content: space-between;
    padding: 1rem;
}
.title{
    margin: 0 auto;
}
.create-task-btn{
    border: none;
    outline: none;
    padding: .5rem .7rem;
    color: #fff;
    background-color: #109230;
    border-radius: 5px;
    cursor: pointer;
}
.close-btn{
     border: none;
    outline: none;
    padding: .5rem .7rem;
    color: #fff;
    background-color: red;
    border-radius: 5px;
    cursor: pointer;
}
</style>