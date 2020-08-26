<template>
<div>
  <Header />
  <AddTodo @add-todo="addTodo"/>
  <Todos v-bind:propsFromApp="todos" @del-todo="delTodo"/>
</div>
</template>

<script>
import Todos from "./components/Todos";
import Header from "./components/Layout/Header";
import AddTodo from "./components/AddTodo";
import axios from "axios";

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data(){
    return {
      todos: []
    }
  },
  methods: {
    delTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => {
          this.todos = this.todos.filter(el => el.id !== id)
          console.log(res);
        })
        .catch(err => console.log(err));
    },
    addTodo(newTodo){
      const {title, completed} = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title, completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=52')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err))
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Avenir, Helvetica, Arial, sans-serif;
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
  .btn:hover {
    background: #666;
  }

</style>
