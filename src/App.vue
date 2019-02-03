<template>
  <div class="container">
    <nav>
      <div class="nav nav-tabs nav-fill mt-2" id="nav-tab">
        <a class="nav-item nav-link active" id="nav-todo-tab" data-toggle="tab" href="#nav-todo" @click="Canceled">
          <router-link to="/todo">СДЕЛАТЬ</router-link>
        </a>
        <a class="nav-item nav-link" id="nav-done-tab" data-toggle="tab" href="#nav-done" @click="Canceled">
          <router-link to="/done">ВЫПОЛНЕНО</router-link>
        </a>
      </div>
    </nav>

    <div class="tab-content" id="nav-tabContent">
      <div class="tab-pane fade show active" id="nav-todo">
        <new-item-form @click="Canceled" @submit="NewTodo"/>
        <div v-for="(todo, index) in todoList" :key="todo.id">
          <todo-item v-if="!todo.maked" :todo="todo" :chooseId="chooseId" :index="index"
                     @del="todoList.splice(index,1)"
                     @choose="ChooseItem" @change="ChangeName" @canceled="Canceled" @check="chooseId = -1"/>
        </div>
      </div>

      <div class="tab-pane fade" id="nav-done">
        <input type="button" class="btn btn-outline-secondary btn-block mt-2" value="Удалить все"
               @click="DelAllDone"/>
        <div class="scroll-area">
          <div v-for="(todo, index) in todoList" :key="todo.id+'a'">
            <todo-item v-if="todo.maked" :todo="todo" :chooseId="chooseId" :index="index" class="todo_item"
                       @del="todoList.splice(index,1)"
                       @choose="ChooseItem" @change="ChangeName" @canceled="Canceled" @check="chooseId = -1"/>
          </div>
        </div>
      </div>
    </div>
    {{ $route.params.type }}
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
        if (this.someDone && window.confirm("Удалить все выполненные?")) {
          for (let i = 0; i < this.todoList.length; i++) {
            if (this.todoList[i].maked) {
              this.todoList.splice(i, 1);
              this.chooseId = -1;
              i--
            }
          }
        }
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
    },
    computed: {
      someDone() {
        let someDone = 0;
        for (var i = 0; i < this.todoList.length; i++) someDone += this.todoList[i].maked;
        return someDone;
      }
    }
  }
</script>