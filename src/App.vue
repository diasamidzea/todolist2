<template>
  <div>
    <new-item-form  @submit="NewTodo" />
    <h3>Не выполнено</h3>
    <div v-for="(todo, index) in todoList" :key="todo.id">
      <todo-item v-if="!todo.maked" :todo="todo" :chooseId="chooseId" :index="index" @del="todoList.splice(index,1)"
                 @choose="ChooseItem" @change="ChangeName" @canceled="Canceled"/>
    </div>
    <h3>
      Выполнено
      <input type="button" value="Удалить все" @click="DelAllDone"  />
    </h3>
    <div v-for="(todo, index) in todoList" :key="todo.id+'a'">
      <todo-item v-if="todo.maked" :todo="todo" :chooseId="chooseId" :index="index" @del="todoList.splice(index,1)"
                 @choose="ChooseItem" @change="ChangeName" @canceled="Canceled"/>
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
        methods:{
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
                for ( let i=0; i<this.todoList.length; i++) {
                    if (this.todoList[i].maked) {
                        this.todoList.splice(i,1);
                        i--
                    }
                }
            },
            NewTodo(newTodoName) {
                if (newTodoName) {
                    this.todoList.push({
                        id: (this.todoList[this.todoList.length-1].id+1),
                        maked: false,
                        name: newTodoName
                    })
                }
            }
        }
    }
</script>
