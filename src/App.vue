<template>
  <div class="container-fluid main_div">

    <div class="navbar-fixed-top">
      <ul class="nav nav-tabs">
        <li class="nav-item">
          <a @click="Canceled" class="nav-link active" id="todo-tab" data-toggle="tab" href="#todo"
             aria-selected="true">Не сделано</a>
        </li>
        <li class="nav-item">
          <a @click="Canceled" class="nav-link" id="done-tab" data-toggle="tab" href="#done"
             aria-selected="false">Сделано</a>
        </li>
      </ul>
    </div>

    <div class="tab-content">
      <div class="tab-pane active" id="todo">
        <new-item-form class="top_of_scroll fixed-top" @submit="NewTodo"/>
        <div v-for="(todo, index) in todoList" :key="todo.id">
          <todo-item v-if="!todo.maked" :todo="todo" :chooseId="chooseId" :index="index" class="todo_item"
                     @del="todoList.splice(index,1)"
                     @choose="ChooseItem" @change="ChangeName" @canceled="Canceled" @check="chooseId = -1"/>
        </div>
      </div>

      <div class="tab-pane" id="done">
        <input type="button" class="btn btn-outline-danger btn-block top_of_scroll fixed-top" value="Удалить все"
               @click="DelAllDone"/>
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
        if (this.chooseId === -2) {
          for (let i = 0; i < this.todoList.length; i++) {
            if (this.todoList[i].maked) {
              this.todoList.splice(i, 1);
              this.chooseId = -1;
              i--
            }
          }
        } else this.chooseId = -2
      },
      NewTodo(newTodoName) {
        if (newTodoName) {
          this.todoList.push({
            id: this.todoList.length ? (this.todoList[this.todoList.length - 1].id + 1) : 1,
            maked: false,
            name: newTodoName
          })
        }
      }
    }
  }
</script>

<style>

  html, body {
    height: 100%;
  }

  body {
    display: flex;
  }

</style>

<style scoped>

  .main_div {
    display: flex;
    flex-direction: column;
    flex: 1 1 auto;
    padding: 0;
  }

  .tab-content {
    display: flex;
    flex-direction: column;
    flex: 1 1 auto;
  }

  .tab-pane {
    overflow: auto;
  }

  .top_of_scroll {
    position: sticky;
    top: 0;
  }

  .todo_item {
    margin-top: 2px;
  }

</style>