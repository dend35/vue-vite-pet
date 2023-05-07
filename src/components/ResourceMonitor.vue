<script setup lang="ts">
import {reactive, ref} from "vue";
import ResourceMonitorSwitchButton from "./ResourceMonitor/ResourceMonitorSwitchButton.vue";
import ChartJS from "./ChartJS.vue";
const _state = reactive({
    metrics: [],
    values: []
})
function updateMetric(e){
    const value = e.target.innerHTML
    const exists = _state.metrics.some(i => i === value)
    if(exists){
        _state.metrics = _state.metrics.filter(i => i != value)
    }else {
        _state.metrics.push(value)
    }
}
function updateValue(e){
    console.log(e)
    const value = e.target.innerHTML
    console.log(value, _state)
    const exists = _state.values.some(i => i === value)
    if(exists){
        _state.values = _state.values.filter(i => i != value)
    }else {
        _state.values.push(value)
    }
}

function isActive(item){
    return _state.metrics.some(i => i == item) || _state.values.some(i => i == item)
}
</script>

<template>
  <div class="rm">
      <div class="rm-menu-side">
          <ResourceMonitorSwitchButton value="CPU" :active="isActive('CPU')" @click="updateMetric"/>
          <ResourceMonitorSwitchButton value="GPU" :active="isActive('GPU')" @click="updateMetric"/>
          <ResourceMonitorSwitchButton value="RAM" :active="isActive('RAM')" @click="updateMetric"/>
          <ResourceMonitorSwitchButton value="ROM" :active="isActive('ROM')" @click="updateMetric"/>
      </div>
      <div>
      <div class="rm-menu-top">
          <ResourceMonitorSwitchButton class="rm-menu-top-item" value="Temp" :active="isActive('Temp')" @click="updateValue"/>
          <ResourceMonitorSwitchButton class="rm-menu-top-item" value="Load" :active="isActive('Load')" @click="updateValue"/>
          <ResourceMonitorSwitchButton class="rm-menu-top-item" value="All" :active="isActive('All')" @click="updateValue"/>
      </div>
          
      <div class="rm-content">
          <ChartJS></ChartJS>
      </div>
      </div>
  </div>
    
</template>

<style scoped>
.rm-btn{
    border-radius: 10px;
    transition: .3s;
    user-select: none;
    cursor: pointer;
    border: 2px solid #747bff;
    padding: 2px;
    background-color: #242424;
}
.rm-btn:hover{
    border: 2px solid #b43636;
}
.rm-btn-active{
    border: 2px solid rgba(54, 180, 56, 0.33) !important;
}
.rm{
    background-color: #1a1a1a;
    display: flex;
    height: 40vh;
    border-radius: 10px;
    padding: 10px;
}
.rm-menu-side{
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    margin-top: 2rem;
    gap: 5px;
    
}
.rm-menu-side-item{
    font-size: 1.5rem;
}
.rm-menu-side-item:hover{
    
}

.rm-menu-top-item{
    font-size: 1.5rem;
    width: 20%;
}
.rm-menu-top{
    display: flex;
    gap: 5px;
}

.rm-content{
    width: 40vw;
    height: 50%;
}
</style>