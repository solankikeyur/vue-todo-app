<script setup>
defineProps({
    filterInput: String
});
const emit = defineEmits(["filterTask"]);
</script>

<template>
  <div class="row">
    <div class="col-md-3 col-lg-3"></div>
    <div class="col-md-6 col-lg-6 col-12" >
      <button class="btn btn-xs btn-outline-primary" :class="filterInput === 'all' ? 'bg-primary text-white' : ''" @click="emit('filterTask', 'all')">All</button>
      <button class="btn btn-xs btn-outline-success" :class="filterInput === 'completed' ? 'bg-success text-white' : ''" @click="emit('filterTask', 'completed')">Completed</button>
      <button class="btn btn-xs btn-outline-danger" :class="filterInput === 'remaining' ? 'bg-danger text-white' : ''" @click="emit('filterTask', 'remaining')">Remaining</button>
    </div>
    <div class="col-md-3 col-lg-3"></div>
  </div>
</template>
<style>
.btn {
  margin-right: 10px;
}
</style>
