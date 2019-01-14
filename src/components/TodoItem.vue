<template>
  <div class="row btn-group">

    <button class="col-1 btn btn-success">
      <input type="checkbox" v-model="todo.maked" @click="$emit('check')"/>
    </button>

    <button class="col-10 btn btn-info disabled">
      <div class="todo_name" @click="$emit('choose', todo.id)" v-if="(todo.id !== chooseId)">
        {{ todo.name }}
      </div>
      <form class="row" v-if="(todo.id === chooseId)" @submit.prevent="ChangeName">
        <input class="col-7" v-model="newName"/>
        <input class="col-2 btn btn-success" type="submit" value="ok"/>
        <input class="col-3 btn btn-warning" type="button" @click="$emit('canceled'); newName = todo.name"
               value="cancel"/>
      </form>
    </button>

    <button class="col-1 btn btn-danger btn-block" @click="$emit('del')">x</button>

  </div>
</template>

<script>
  export default {
    props: ["todo", "chooseId", "index"],
    data() {
      return {
        newName: this.todo.name,
      }
    },
    methods: {
      ChangeName() {
        this.$emit("change", [this.newName, this.index])
      }
    }
  }
</script>

<style scoped>
  div {
    margin: 0;
    width: 100%;
  }

  form {
    margin: 0;
  }

  .btn {
    padding: 0;
  }

  .todo_name {
    text-align: left;
    padding-left: 10px;
  }
</style>