<template>
  <div id="app">
    <Todos 
    v-bind:myPropsForBinding="todos"
    v-on:del-todo="deleteTodo"
    />
  </div>
</template>

<script>
import Todos from "./components/Todos"


export default {
  name: 'App',
  components: {
    Todos
  },
  methods: {
    deleteTodo(id){
      this.todos = this.todos.filter(el => el.id !== id);
    }  
  },
  data(){
    return{
      todos: [
        {
          id: 1,
          title: "Todo 1",
          completed: false
        },
        {
          id: 2,
          title: "Todo 2",
          completed: true
        },

        {
          id: 3,
          title: "Todo 3",
          completed: false
        }
      ]
    }
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
</style>
