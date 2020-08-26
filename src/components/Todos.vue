<template>
<div>
    <p v-for="todo in propsFromApp" v-bind:key="todo.id">
    <TodoItem v-bind:oneTodo="todo" @del-todo="$emit('del-todo', todo.id)"/>
    </p>
</div>
</template>

<script>
import TodoItem from "./TodoItem"

export default {
    name: "Todos",
    props: ["propsFromApp"],
    components: {
        TodoItem
    }

}
</script>

<style scoped>

</style>