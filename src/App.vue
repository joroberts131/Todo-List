<script setup>
  import { ref } from 'vue'
  const msg = ref('Hello World!')
  const list = ref([1,2,3,4,5])
  function addToList(str) {
    list.value.push(str)
    msg.value = ''
  }
  function removeFromList() {
    list.value.pop()
  }
</script>

<template>
  <body>
    <h1>To-Do app</h1>
    <p></p>
    <div class = "container">
      <input class = "box" type="text" v-model="msg">
      <p>{{ msg }}</p>
      <button class = "add" @click="addToList(msg)">Add to list</button>
      <button @click="removeFromList()">Pop</button>
    </div>
    <ul>
      <li v-for="item in list">{{item}}</li>
    </ul>
  </body>
</template>

<style>
  .box {
    width: 20%;
    height: 25px;
    border: 3px solid #5f2d2c;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 10px;
    background-color: #c1715f;
    
  }
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    
  }
  body {
    background-color: tan;
  }
  .add {
    margin: auto;
    background-color: #c1715f;
  }
  h1 {
    margin: auto;
    width: 25%;
    border: 5px solid #5f2d2c;
    padding: 10px;
    color:  #5f2d2c;
    font-size: 40px;
    text-align: center;
    background-color: #c1715f;
    
  }
</style>

