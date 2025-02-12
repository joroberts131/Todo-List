<script setup>
  import { ref } from 'vue'
  const msg = ref('')
  const list = ref([1,2,3,4,5])
  let listSave = localStorage.setItem("list", JSON.stringify(list.value))
  list.value = JSON.parse(localStorage.getItem("list"))
  function addToList(str) {
    listSave = localStorage.setItem("list", JSON.stringify(list.value))
    console.log("Data saved! " + JSON.parse(localStorage.getItem("list")))
    console.log(str)
    if(str == ""){
      list.value.push(Math.floor(Math.random() * 100000))
    }else{
      list.value.push(str)
      msg.value = ''
    }
  }
  function removeFromList(item) {
    listSave = localStorage.setItem("list", JSON.stringify(list.value))
    let index = list.value.indexOf(item)
    list.value.splice(index, 1)
  }
  function finish(item){
    let index = list.value.indexOf(item)
    let str = item.toString()
    console.log(index + " " + item + " test")
    if(str.startsWith("Done: ")){
      list.value.splice(index, 1, str.slice(6))
    }else{
      list.value.splice(index, 1, "Done: " + str)
    }
    
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
  .done {
    text-decoration: line-through;
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

