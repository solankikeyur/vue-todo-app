<script setup>
import { onMounted, ref, computed } from "vue";
import TodoItem from "./components/TodoItem.vue";
import TodoFilter from "./components/TodoFilter.vue";

const task = ref("");
const todos = ref([]);
const filterValue = ref("all");

const filteredTodos = computed(() => {
  if(filterValue.value === "all") {
    return todos.value;
  } else if(filterValue.value === "completed") {
    return todos.value.filter((todo) => todo.done === true);
  } else if(filterValue.value === "remaining") {
    return todos.value.filter((todo) => todo.done === false);
  }
})

const addTask = () => {
  if (!task.value) {
    alert("Please enter task.");
    return false;
  }
  todos.value.push({ name: task.value, done: false });
  localStorage.setItem("todos", JSON.stringify(todos.value));
  task.value = "";
}

const deleteTask = (index) => {
  todos.value = todos.value.filter((todo, i) => i !== index);
  localStorage.setItem("todos", JSON.stringify(todos.value));
}

onMounted(() => {
  if (localStorage.getItem("todos")) {
    todos.value = JSON.parse(localStorage.getItem("todos"));
  }
});

const updateTask = (index) => {
  localStorage.setItem("todos", JSON.stringify(todos.value));
}

const filterTask = (value) => {
  filterValue.value = value;
}

</script>

<template>
  <div class="container main">
    <div class="row">
      <div class="col-12">
        <div class="h1 text-center">Todo App</div>
      </div>
    </div>

    <div class="row mt-4">
      <div class="col-12">
        <div class="form-group">
          <input type="text" class="form-control" v-model="task" />
        </div>
      </div>
    </div>
    <button class="btn btn-primary mt-2" @click="addTask">Add</button>
    <hr />

    <div class="container">
      <div class="row">
        <div class="col-md-3 col-lg-3"></div>
        <div class="col-12 col-md-6 col-lg-6">
          <ul class="list-group">
            <TodoItem :todos="filteredTodos" @update-task="updateTask" @delete-task="deleteTask"></TodoItem>
          </ul>
        </div>
        <div class="col-md-3 col-lg-3"></div>
      </div>
      <TodoFilter @filter-task="filterTask" :filterInput="filterValue" ></TodoFilter>
    </div>
    <hr />
  </div>
</template>

<style>
.main {
  background-color: #03001C;
}
.h1 {
  color: #B6EADA;
  background-color: #301E67;
  margin: 10px;
  padding: 10px;
}
</style>