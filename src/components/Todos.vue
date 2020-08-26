<template>
    <div>
        <div v-for="todo in myPropsForBinding" v-bind:key="todo.id">
            <TodoItem 
            v-bind:todoItem="todo"
            v-on:del-todo="$emit('del-todo', todo.id)"
            />
        </div>
    </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
    name: "Todos",
    props: ["myPropsForBinding"],
    components: {
        TodoItem
    },
}
</script>

<style scoped>

</style>