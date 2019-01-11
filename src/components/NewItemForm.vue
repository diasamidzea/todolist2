<template>
  <div>
    <form @submit.prevent="NewTodo">
      <div class="input-group input-group-inherit">
        <input type="text" v-model="newTodoName" class="form-control" placeholder="Введите новую задачу">
        <div type="submit" class="input-group-text">OK</div>
      </div>
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