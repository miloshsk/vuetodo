<template>
  <div id="app">
    <todo-form @getTask="addTaskToList"></todo-form>
    <ul>
      <todo-item v-for="(item, index) in todoList"
                :key="index"
                :index="index"
                :todoItem="item.value"
                :taskDone="item.taskDone"
                @newItemValue="newItemValue"
                @removeItem="removeItem"
                @changeTaskToggle="changeTaskToggle"
      ></todo-item>
    </ul>
  </div>
</template>

<script>
import todoForm from './components/todoForm.vue'
import todoItem from './components/todoItem.vue'

export default {
  components: {
    todoForm,
    todoItem
  },
  data() {
    return {
      todoList: []
    }
  },
  methods: {
    addTaskToList(value) {
      this.todoList.push({
        value: value,
        taskDone: false
      });
    },
    newItemValue(val, index) {
      this.todoList[index].value = val;
    },
    removeItem(index) {
      this.todoList.splice(index,1);
    },
    changeTaskToggle(val, index) {
        this.todoList[index].taskDone = val;
    }
  }
}
</script>

<style lang="sass">
  *
    box-sizing: border-box
  body 
    background-color: #F5F5F5
  #app
    width: 500px
    margin: 0 auto
    font-size: 24px
    background-color: #fff
    padding: 5px
    border-radius: 5px
  ul
    list-style-type: none
    padding: 0
</style>
