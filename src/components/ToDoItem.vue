<template>
  <li>
    {{ task }}
    <button @click="deleteTask">X</button>
  </li>
</template>

<script>
export default {
  props: ["task"],

  methods: {
    deleteTask() {
      this.$emit("taskDeleted");
    },
  },
};
</script>

<style></style>
