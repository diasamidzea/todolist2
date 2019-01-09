<template>
    <div class="todo-style">
        <span @click="$emit('choose')" v-if="(todo.id !== chooseId)">
            {{ todo.name }}
        </span>
        <form v-if="(todo.id === chooseId)" @submit.prevent="ChangeName" class="todo-style">
            <input v-model="newName"/>
            <input type="submit" value="ok"/>
            <input type="button" @click="$emit('canceled'); newName = todo.name" value="cancel"/>
        </form>
    </div>
</template>

<script>
    export default {
        props: ["todo", "chooseId"],
        data() {
            return {
                newName: this.todo.name,
            }
        },
        methods: {
            ChangeName() {
                this.$emit("change", this.newName)
            }
        }
    }
</script>

<style scoped>
    .todo-style {
        display: inline;
    }
</style>