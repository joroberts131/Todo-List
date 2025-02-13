<script setup>
import { ref } from 'vue'
const msg = ref('')
const list = ref([])
// Load saved list from localStorage or use default if none exists
const savedList = localStorage.getItem("list")
list.value = savedList ? JSON.parse(savedList) : [1, 2, 3, 4, 5]

// Add item to list
function addToList(str) {
  // If string is empty adds random number for testing purposes, otherwise adds string
  str == "" ? list.value.push(Math.floor(Math.random() * 100000)) : list.value.push(str)
  // Clears message
  msg.value = ''
  // Save list to localStorage
  localStorage.setItem("list", JSON.stringify(list.value))
  // Logs saved list to console
  console.log("Data saved! " + JSON.parse(localStorage.getItem("list")))
}
// Removes item from list
function removeFromList(item) {
  // Index of item to be removed
  let index = list.value.indexOf(item)
  // Removes item from list
  list.value.splice(index, 1)
  // Save list to localStorage
  localStorage.setItem("list", JSON.stringify(list.value))
  console.log("Data saved! " + JSON.parse(localStorage.getItem("list")))
}
// Lets you mark items as complete 
function finish(item) {

  let index = list.value.indexOf(item)
  let str = item.toString()
  // Checks if item is already complete if so romoves checkmark designation otherwise checks it off
  if (str.startsWith("✓")) {
    list.value.splice(index, 1, str.slice(1, str.length - 1))
  } else {
    list.value.splice(index, 1, "✓" + str + "✓")
  }
  // Save list to local storage
  localStorage.setItem("list", JSON.stringify(list.value))
}
// Used to determine if an item is complete returning true or false
function itemCheck(item) {
  let str = item.toString()
  return str.startsWith("✓")
}
// Clears the list
function clearList(){
  list.value = []    
  // Save list to local storage
  localStorage.setItem("list", JSON.stringify(list.value))
}
</script>

<template>
  <body>
    <h1>To-Do app</h1>
    <!--Spacer-->
    <p></p>
    <!--Input box and button-->
    <div class="container">
      <input placeholder="Enter Task Here..." class="box" type="text" v-model="msg">
      <button class="click" @click="addToList(msg)">Add to list</button>
      <button class="click" @click="clearList()">Clear List</button>
    </div>
    <ul>
      <!-- Iterates through all items in a list -->
      <li v-for="item in list">
        <!-- V-if statement to determine if an item should have its text struckthrough-->
        <div v-if="itemCheck(item)" class="done">
          <button class="click" @click="removeFromList(item)">X</button>
          {{ item }}
          <button class="click" @click="finish(item)">✓</button>
        </div>
        <div v-else>
          <button class="click" @click="removeFromList(item)">X</button>
          {{ item }}
          <button class="click" @click="finish(item)">✓</button>
        </div>
      </li>
    </ul>
  </body>
</template>

<style>
::placeholder {
  color: #5f2d2c;
}

li {
  width: 80%;
  height: 18px;
  border: 3px solid #5f2d2c;
  border-radius: 5px;
  padding: 7px;
  margin-bottom: 5px;
  background-color: #c1715f;
  list-style: none;
  margin: auto;
  font-size: 20px;
  text-align: left;
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
  display: inline-block !important;;
  margin: auto;
  background-color: #c1715f;
}

h1 {
  margin: auto;
  width: 25%;
  border: 5px solid #5f2d2c;
  padding: 10px;
  color: #5f2d2c;
  font-size: 40px;
  text-align: center;
  background-color: #c1715f;

}
</style>

