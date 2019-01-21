<template>
  <form class="input-group mt-2" @submit.prevent="NewTodo">
    <input type="text" class="form-control" placeholder="Введите новое задание" v-model="newTodoName"
           @click="$emit('click')"/>
    <div class="input-group-append">
      <button class="btn btn-outline-secondary border" type="submit" @click="$emit('click')">ОК</button>
    </div>
  </form>
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