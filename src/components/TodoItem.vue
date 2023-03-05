<script setup>
defineProps({
  todos: Array,
});
const emit = defineEmits(["updateTask", "deleteTask"]);

</script>
<template>
  <li
    class="list-group-item mb-2 strike"
    v-if="todos.length > 0"
    v-for="(todo, index) in todos"
    :key="index"
  >
    <input
      class="form-check-input"
      v-model="todo.done"
      type="checkbox"
      @change="emit('updateTask', index)"
    />
    <del v-if="todo.done">{{ todo.name }}</del>
    <span v-else>{{ todo.name }}</span>
    <button class="badge bg-danger float-end" @click="emit('deleteTask', index)" >Delete</button>
  </li>
  <li class="list-group-item mb-2" v-else>No todo found. You can add one.</li>
</template>

<style>
  input {
    margin-right: 20px;
  }
  .list-group-item {
    background-color: #B6EADA;
    color: #301E67;
  }
</style>