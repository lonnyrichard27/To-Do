<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from './components/Todos.vue';
import Header from './components/layout/Header';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
      deleteTodo(id) {
        this.todos = this.todos.filter(todo => todo.id !== id );
      },
      addTodo(newTodo) {
        this.todos = [...this.todos, newTodo]; 
      }
      },
       created (){
        // fetch('https://jsonplaceholder.typicode.com/todos/1')
        //   .then(response => this.todos = response.data)
        //   .then(json => console.log(json))
        // .catch(err => (console.log(err)));

        axios.get('https://jsonplaceholder.typicode.com/todos')
          .then(res => this.todos = res.data)
          .catch(err => console.log(err));
    }
}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover{
  background: #666;
}
</style>
