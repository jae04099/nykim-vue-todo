<template>
  <div id="app">
    <TodoHeader />
    <TodoTitle :propsdata="checkCount" />
    <TodoInput @addItem="addOneItem" />
    <TodoController @removeAll="removeAll" @sortItem="sortAllItem" @clearAll="clearAllItem"/>
    <TodoList
      :propsdata="todoItems"
      @toggleItem="toggleComplete"
      @removeItem="removeTodo"
    />
    <TodoFooter />
  </div>
</template>

<script>
import TodoInput from "./components/TodoInput";
import getDate from "./assets/commonJS/getDate";
import TodoTitle from "./components/TodoTitle";
import TodoHeader from "./components/TodoHeader";
import TodoController from "./components/TodoController";
import TodoFooter from "./components/TodoFooter";
import TodoList from "./components/TodoList";

export default {
  name: "App",
  data() {
    return {
      todoItems: [],
    };
  },
  components: {
    TodoInput,
    TodoTitle,
    TodoHeader,
    TodoController,
    TodoFooter,
    TodoList,
  },
  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          this.todoItems.push(
            JSON.parse(localStorage.getItem(localStorage.key(i)))
          );
        }
      }
    }
  },
  computed: {
    checkCount() {
      const checkLeftItems = () => {
        let leftCount = 0;
        for (let i = 0; i < this.todoItems.length; i++) {
          if (this.todoItems[i].completed === false) {
            leftCount++;
          }
        }
        return leftCount;
      };
      const count = {
        total: this.todoItems.length,
        left: checkLeftItems(),
      };
      return count;
    },
  },
  methods: {
    addOneItem(todoItem) {
      let value = {
        item: todoItem,
        date: `${getDate().date} ${getDate().week}`,
        time: getDate().time,
        completed: false,
      };
      localStorage.setItem(todoItem, JSON.stringify(value));
      this.todoItems.push(value);
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleComplete(todoItem) {
      todoItem.completed = !todoItem.completed;
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    removeAll() {
      this.todoItems = [];
      localStorage.clear();
    },
    sortTodoLatest(){
      this.todoItems.sort(function(a, b){
        return b.time - a.time;
      })
    },
    sortTodoOldest(){
      this.todoItems.sort(function(a, b){
        return a.time - b.time
      })
    },
    sortAllItem(selectedSort){
      if(selectedSort.value === "date-desc"){
        this.sortTodoLatest();
      }else if(selectedSort.value === "date-asc"){
        this.sortTodoOldest();
      }
    },
    mounted(){
      this.sortTodoOldest()
    }
  },
};
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