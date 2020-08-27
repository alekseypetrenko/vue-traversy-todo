<template>
<div >
    <p v-for="todo in propsFromApp" :key="todo.id">
        <TodoItem :todo="todo" @del-todo="$emit('del-todo', todo.id)"/>
    </p>

</div>
</template>

<script>
import TodoItem from "./TodoItem";

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