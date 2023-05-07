<script setup>
import {reactive, ref} from "vue";

let addItem = reactive({
    status: ''
});
const list = ref([
    {title: "test1", text: "test1_text_wip", status: "wip"},
    {title: "test2", text: "test2_text_completed", status: "completed"},
])
function complete(item){
    console.log(item)
    item.status = "completed"
}

function remove(item){
    list.value = list.value.filter(i => i.title !== item.title)
}

function add(item) {
    if(!item.title)
        return
    console.log(item)
    list.value.push(item);
    addItem = {};
}
</script>
<template>
  <div class="todos">
      <div class="items">
          <div v-for="item in list" class="item">
              <div class="item-left">
                  <div class="item-header">{{item.title}} {{item.status}}</div>
                  <div class="item-body">{{item.text}}</div>
              </div>
              <div class="item-right">
                  <button class="item-btn" @click="complete(item)">Complete</button>
                  <button class="item-btn delete" @click="remove(item)">Delete</button>
              </div>
          </div>
      </div>
      <div class="item-add">
          <div style="flex: 100 1 auto; display: flex; flex-direction: column">
              <div style="display: flex">
                  <input
                      style="flex: 2 0 auto;"
                      v-model="addItem.title"
                      placeholder="Заголовок"
                  />
                  <select 
                      v-model="addItem.status" style="flex: 1 0 auto;">
                      <option value="" selected hidden>Status</option>
                      <option value="new">New</option>
                      <option value="wip">WIP</option>
                      <option value="completed">Completed</option>
                  </select>
              </div>
              <textarea
                  v-model="addItem.text"
                  placeholder="Описание"
                  autocomplete="off"
                  class="item-add-input"
                  spellcheck="true"
                  style="resize: none"
              /> 
          </div>
          <button class="item-add-btn" @click="add(addItem)">Submit</button>
      </div>
  </div>
</template>
<style>
.todos{
    background-color: #1a1a1a;
    position: relative;
    width: 30vw;
    height: 40vh;
    overflow: hidden;
    border-radius: 10px;
    padding: 10px;
}
.item{
    border: 2px solid rgba(255, 255, 255, .1);
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 3px;
    padding-left: 10px;
    align-items: center;
}
.item-left{
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}
.item-right{
    display: flex;
    gap: 5px;
}
.item-header{
    font-size: 1.2rem;
}
.item-body{
    
}
.item-btn{
    border: 2px solid #535bf2;
    transition: .3s;
    z-index: auto;
    filter: drop-shadow(0 0 0px #000000);
    user-select: none;
}
.item-btn:hover{
    transform: scale(.95);
    filter: drop-shadow(0 0 20px #535bf2);
    z-index: 100;
}

.item-btn.delete{
    border: 2px solid rgba(182, 2, 2, 0.67);
}
.item-btn.delete:hover{
    filter: drop-shadow(0 0 20px rgba(182, 2, 2, 1));
}

.item-add{
    position: absolute;
    width: 100%;
    bottom: 0;
    //margin-top: auto;
    display: flex;
    gap: 5px;
    margin: 3px;
}
.item-add-input{
    height: 70px;
}
.item-add-btn{
    flex: 1 1 auto;
    border: 2px solid rgba(255, 255, 255, .1);
    margin-right: 5px;
}
</style>