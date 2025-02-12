<script setup>
  import { ref } from 'vue'
  const msg = ref('')
  const list = ref([1,2,3,4,5])
  function addToList(str) {
    console.log(str.value)
    if(str == ""){
      list.value.push(Math.floor(Math.random() * 100000))
    }else{
      list.value.push(str)
      msg.value = ''
    }
  }
  function removeFromList(str) {
    list.value.pop()
  }
  function finish(item){
    index = list.value.indexOf(item)
    console.log(index + " " + item + " test")
    list.value = list(list.indexOf(item)).value + ' (done)'
    
  }
</script>

<template>
  <body>
    <h1>To-Do app</h1>
    <p></p>
    <div class = "container">
      <input placeholder="Enter Task Here..." class = "box" type="text" v-model="msg">
      <p>{{ msg }}</p>
      <button class = "click" @click="addToList(msg)">Add to list</button>
      <button @click="removeFromList(msg)">Pop</button>
    </div>
    
    <ul>
      <li v-for="item in list">
        {{item}} 
        <button class = "click" @click="removeFromList(item)">x</button>
        <input type = "checkbox" @change="finish(item)">
      </li>  
    </ul>
  </body>
</template>

<style>
  ::placeholder{
    color: #5f2d2c;
  }
  .box {
    width: 20%;
    height: 25px;
    border: 3px solid #5f2d2c;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 10px;
    background-color: #c1715f;
    font-size: 20px;
    
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
  .click {
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

