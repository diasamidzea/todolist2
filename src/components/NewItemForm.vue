<template>
    <div>
        <form @submit.prevent="NewTodo">
            <input v-model="newTodoName" placeholder="Введите задание"/>
            <input type="submit" value="+"/>
        </form>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                newTodoName: ""
            }
        },
        methods: {
            NewTodo() {
                this.$emit("submit", this.newTodoName)
                this.newTodoName = ""
            }
        }
    }
</script>