<template>
  <form class="input-group mt-2" @submit.prevent="ChangeName">
    <div class="input-group-prepend">
      <span class="input-group-text"><input type="checkbox" v-model="todo.maked" @click="$emit('check')"/></span>
    </div>
    <input type="text" class="form-control" disabled v-if="(todo.id !== chooseId)" v-model="newName"/>
    <input type="text" class="form-control" v-if="(todo.id === chooseId)" v-model="newName"/>
    <div class="input-group-append" id="button-addon4">
      <button class="btn btn-outline-secondary border" type="submit" v-if="(todo.id === chooseId)">
        <i class="far fa-check-circle"></i>
      </button>
      <button class="btn btn-outline-secondary border" type="button" v-if="(todo.id === chooseId)"
              @click="$emit('canceled'); newName = todo.name">
        <i class="far fa-times-circle"></i>
      </button>
      <button class="btn btn-outline-secondary border" type="button" v-if="(todo.id !== chooseId)"
              @click="$emit('choose', todo.id)">
        <i class="far fa-edit"></i>
      </button>
      <button class="btn btn-outline-secondary border" type="button" @click="$emit('del')">
        <i class="far fa-trash-alt"></i>
      </button>
    </div>
  </form>
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