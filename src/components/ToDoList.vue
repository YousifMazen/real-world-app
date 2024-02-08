<template>
  <ul>
    <label>Enter new task: </label>
    <input type="text" v-model="enteredTask" @keypress.enter="addTask" />
    <button @click="addTask">Add</button>
    <br />
    <h1>{{ errorMessage }}</h1>
    <to-do-item
      v-for="(task, index) in toDos"
      :key="index"
      :task="task"
      @taskDeleted="deleteTask(index)"
    />
  </ul>
</template>

<script>
import ToDoItem from "../components/ToDoItem.vue";
export default {
  data() {
    return {
      toDos: [],
      enteredTask: "",
      errorMessage: "",
    };
  },

  methods: {
    addTask() {
      if (this.enteredTask.length > 0) {
        this.toDos.push(this.enteredTask);
        this.enteredTask = "";
        this.errorMessage = "";
      } else {
        this.errorMessage = "Type a task first";
      }
    },

    deleteTask(index) {
      this.toDos.splice(index, 1);
    },
  },

  components: {
    "to-do-item": ToDoItem,
  },
};
</script>

<style scoped>
h1 {
  color: brown;
}
</style>
