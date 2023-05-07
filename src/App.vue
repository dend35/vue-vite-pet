<script setup lang="ts">
import ToDoList from "./components/ToDoList.vue";
import ResourceMonitor from "./components/ResourceMonitor.vue";
import ChartJS from "./components/ChartJS.vue";
</script>

<template>
    <div class="main">
        <ToDoList></ToDoList>
        <ResourceMonitor></ResourceMonitor>
<!--        <ChartJS></ChartJS>-->
    </div>
  
</template>

<style scoped>
.main{
    display: flex;
    gap: 10px;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
