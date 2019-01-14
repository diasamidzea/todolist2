<template>
  <div>
    <form class="row" @submit.prevent="NewTodo">
      <input type="text" v-model="newTodoName" class="col-10" placeholder="Введите новую задачу">
      <button type="submit" class="btn btn-success col-2">OK</button>
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
        this.$emit("submit", this.newTodoName);
        this.newTodoName = ""
      }
    }
  }
</script>

<style scoped>
  form {
    margin: 0;
  }
</style>