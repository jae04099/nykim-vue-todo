<template>
  <div id="app">
      <TodoHeader />
        <TodoTitle />
        <TodoInput @addItem="addOneItem"/>
        <TodoController />
        <TodoList :propsdata = "todoItems"/>
      <TodoFooter />
  </div>
</template>

<script>

import TodoInput from "./components/TodoInput"
import getDate from "./assets/commonJS/getDate"
import TodoTitle from "./components/TodoTitle"
import TodoHeader from "./components/TodoHeader"
import TodoController from "./components/TodoController"
import TodoFooter from "./components/TodoFooter"
import TodoList from "./components/TodoList"



export default {
  name: "App",
  data(){
    return{
      todoItems: []
    }
  },
  components: {
    TodoInput,
    TodoTitle,
    TodoHeader,
    TodoController,
    TodoFooter,
    TodoList,

  },
  created(){
    if(localStorage.length > 0){
      for (let i = 0; i < localStorage.length ; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          )
        }
      }
    }
  },
  methods: {
    addOneItem(todoItem){
      let value ={
        item: todoItem,
        date: `${getDate().date} ${getDate().week}`,
        time: getDate().time,
        completed: false
      }
      localStorage.setItem(todoItem, JSON.stringify(value))
      this.todoItems.push(value)
    }
  }
}
</script>
<style lang="scss">
@import "@/assets/style/_reset.scss";
.top {
  width: 100%;
  min-height: 43.6rem;
  padding: 0 $padding 4.5rem;
  background-image: linear-gradient(145deg, #3770cc 20%, #ce91c9 84%);
}
.body {
  padding: 3rem $padding;
  background-color: #efefef;
}
</style>