<script setup>

import {ref,onMounted,computed,watch} from 'vue'

const todos=ref([])
const name = ref('')

const input_content=ref('')
const input_category=ref(null)

const todos_asc=computed(() => todos.value.sort((a,b) => {
  return a.createdAt - b.createdAt
}))





/*----
<<<<<<< HEAD
creating what addTodo can do, adds the todo to the todo array*/


=======
creating what addTodo can do, adds the todo to the todo array gggggg*/
>>>>>>> 99821f66524313cd62387836a6d4888f3de30faa
const addTodo = () => {
  //sheshhh
  if(input_content.value.trim() === '' || input_content.value === null){
    return
  }

  todos.value.push({
    content: input_content.value,
    category: input_category.value,
    createdAt: new Date().getTime(),
    done: false
  })

  /*resets the todo input box*/
  input_content.value=''
  input_category.value= null

}

/*----
creating what removeTodo does, deletes a todo from the array of todos*/
const removeTodo = todo => {
  todos.value=todos.value.filter(t => t!==todo)
}

/*----
adds the todos to the local storage
(any change in todos will be processed by deep*/
watch(todos, newVal => {
  localStorage.setItem('todos',JSON.stringify(newVal))
},{deep:true})  

/*
adds the todo items using localstorage*/
onMounted(() => {
  todos.value = JSON.parse(localStorage.getItem('todos')) || []
})

</script>

<template>
  <main class="app">
    <section class="greeting">
      <h1 class='Title'>
        Hey There!</h1>
      <h3>Ready to do some tasks?</h3>
    </section>

    <section class="create-todo">
      <h3><b>
        CREATE A TODO</b>
      </h3>

      <form @submit.prevent="addTodo">
        <h4>What's on your To-Do List?</h4>
        <input 
          type="text" 
          placeholder="             e.g. read a book" 
          v-model="input_content"/>
        <h4>Pick A Category</h4>
   
        <!--creating an input type of radio to pick one of the listed options (categories)-->

        <div class="options">

          <label>
            <input 
              type="radio"
              name="category"
              value="Organisational"
              v-model="input_category" />
            <span class="bubble Organisational"></span>
            <div><h3>Organisational</h3></div>
          </label>

          <label>
            <input 
              type="radio"
              name="category"
              value="Personal"
              v-model="input_category" />
            <span class="bubble Personal"></span>
            <div><h3>Personal</h3></div>
          </label>

        </div>

        <input type="submit" value="Add To-Do" style="background-image: url('https://upload.wikimedia.org/wikipedia/commons/9/9e/Plus_symbol.svg'); border:none; background-repeat:no-repeat;background-size:17% 100%;" />

      </form>

    </section>

    <section class="todo-list">
      <h3>Your To Do List</h3>
      <div class="list">

        <div v-for="todo in todos_asc" :class="`todo-item ${todo.done && 'done'}`">
          
          <label>
            <input type="checkbox" v-model="todo.done" />
            <span :class="`bubble ${todo.category}`"></span>
          </label>
          
          <div class="todo-content">
            <input type="text" v-model="todo.content">
          </div>
        
          <div class="actions">
            <button class="delete" @click="removeTodo(todo)" style="background-image: url('https://cdn-icons-png.flaticon.com/512/3481/3481306.png'); border:none;background-repeat:no-repeat;background-size:100% 100%"></button>
          </div>

        </div>

      </div>
    </section>

  </main>

</template>
