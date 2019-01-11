<template>
  <div class="container-fluid main-div">

    <div class="navbar navbar-fixed-top">
      <ul class="nav nav-tabs">
        <li class="nav-item">
          <a class="nav-link active" id="todo-tab" data-toggle="tab" href="#todo" aria-selected="true">Не сделано</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" id="done-tab" data-toggle="tab" href="#done" aria-selected="false">Сделано</a>
        </li>
      </ul>
    </div>

    <div class="tab-content">

      <div class="tab-pane active" id="todo">
        <new-item-form @submit="NewTodo"/>
        <div class="scroll-area">
          <div v-for="(todo, index) in todoList" :key="todo.id">
            <todo-item v-if="!todo.maked" :todo="todo" :chooseId="chooseId" :index="index"
                       @del="todoList.splice(index,1)"
                       @choose="ChooseItem" @change="ChangeName" @canceled="Canceled" @check="chooseId = -1"/>
          </div>
        </div>

      </div>


      <div class="tab-pane" id="done">
        <input type="button" class="btn btn-danger btn-block" value="Удалить все" @click="DelAllDone"/>
        <div class="scroll-area">
          <div v-for="(todo, index) in todoList" :key="todo.id+'a'">
            <todo-item v-if="todo.maked" :todo="todo" :chooseId="chooseId" :index="index"
                       @del="todoList.splice(index,1)"
                       @choose="ChooseItem" @change="ChangeName" @canceled="Canceled" @check="chooseId = -1"/>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import NewItemForm from "./components/NewItemForm.vue"
  import TodoItem from "./components/TodoItem.vue"

  export default {
    components: {
      NewItemForm,
      TodoItem
    },
    data() {
      return {
        todoList: [
          {id: 1, maked: false, name: 'Milk'},
          {id: 2, maked: false, name: 'second'}
        ],
        chooseId: -1
      }
    },
    methods: {
      ChooseItem(id) {
        this.chooseId = id
      },
      ChangeName(newName) {
        this.todoList[newName[1]].name = newName[0];
        this.chooseId = -1
      },
      Canceled() {
        this.chooseId = -1
      },
      DelAllDone() {
        for (let i = 0; i < this.todoList.length; i++) {
          if (this.todoList[i].maked) {
            this.todoList.splice(i, 1);
            this.chooseId = -1;
            i--
          }
        }
      },
      NewTodo(newTodoName) {
        if (newTodoName) {
          this.todoList.push({
            id: (this.todoList[this.todoList.length - 1].id + 1),
            maked: false,
            name: newTodoName
          })
        }
      }
    }
  }
</script>

<style>
  /*  html, body {
      height: 100%;
      margin: 0;
      padding: 0;
      overflow: hidden;
      background-color: lightgrey;
    }
    body {
      overflow: auto;  добавить полосу прокрутки
  }*/
  /*html, body {
    height: 100%;
  }*/

  body {
    /*background: rgb(149, 194, 215);*/
  }

  /* .navbar {
     margin-bottom: 0;
   }*/

  .scroll-area {
    overflow: auto;
    max-height: 200px;
    background-color: antiquewhite;
  }

  .main-div {
    padding: 0;
    position: fixed;
    top: 0;
    left: 0;
    /*height: 500px;*/
  }

  .header-item {
    min-height: content-box;
  }

  .body-item {
    overflow: auto;
    min-height: 20%;
    max-height: 70%;
  }
</style>