<template>
  <div>
    <h1>todo list</h1>
    <form @submit.prevent="addNewTodo">
      <label for="todoinput">New todo</label>
      <input v-model="newTodo" type="text" id="todoinput" name="newTodo">
      <button>Add todo</button>
    </form>
    <button @click="allDone">All Done</button>
    <button @click="removeAll">Remove All</button>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <h3 @click="toggleDone(todo)" :class="{done : todo.done}">{{ todo.content }}</h3>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
  </div>
  
</template>

<script>
import { ref } from 'vue';
export default {
  name: 'App',
  setup(){
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo(){
      console.log('form was submitted');
      console.log(newTodo.value);

      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });

      newTodo.value = '';
    }

    function toggleDone(todo){
      todo.done = !todo.done;
    }

    function removeTodo(index){
      todos.value.splice(index, 1);
    }

    function allDone(){
      todos.value.forEach(todo => {
        todo.done = true;
      })
    }

    function removeAll(){
      todos.value = [];
    }

    return{
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      allDone,
      removeAll
    }
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.done{
  text-decoration: line-through;
}
</style>
