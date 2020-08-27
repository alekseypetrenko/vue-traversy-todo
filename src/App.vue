<template>
  <div>
    <Header />
    <AddTodo @add-todo="addTodo"/>
    <Todos :propsFromApp="todos" @del-todo="delTodo"/>
  </div>
</template>

<script>
import axios from "axios";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
import Header from "./components/Layout/Header";

export default {
  name: "App",
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
    addTodo(data){
      const {title, completed} = data;
      axios.post('https://jsonplaceholder.typicode.com/todos', {title, completed})
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err))
    },
    delTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => {
          this.todos = this.todos.filter(el => el.id !== id);
          return res;
        })
        .catch(err => console.log(err))
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
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
