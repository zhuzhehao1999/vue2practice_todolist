<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
        <UserHeader :addTodo="addTodo" />
        <UserList
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
        <UserFooter
          :todos="todos"
          :checkAllTodo="checkAllTodo"
          :clearAllTodo="clearAllTodo"
        />
      </div>
    </div>
  </div>
</template>

<script>
import UserHeader from "./components/UserHeader.vue";
import UserList from "./components/UserList.vue";
import UserFooter from "./components/UserFooter.vue";

export default {
  name: "App",
  components: {
    UserHeader,
    UserList,
    UserFooter,
  },
  data() {
    return {
      //由于todos是MyHeader组件和MyFooter组件都在使用，所以放在App中（状态提升）
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  methods: {
    // add a todo
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    //check or uncheck a todo
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    },
    //delete a todo by ID
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    //all check or all uncheck
    checkAllTodo(done) {
      this.todo.forEach((todo) => {
        todo.done = done;
      });
    },
    clearAllTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.done;
      });
    },
    
  },
  watch: {
      todos: {
        deep: true,
        handler(value) {
          localStorage.setItem("todos", JSON.stringify(value));
        },
      },
    },
};
</script>

<style>
body {
  background-color: #fff;
}
.btn {
  display: inline-block;
  padding: 6px 18px;
  margin: 1px;
  font-size: 16px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.4);
}
.btn-danger {
  color: #fff;
  background-color: rgb(255, 0, 0);
  border: 1px solid #bd362f;
}
.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}
.btn:focus {
  outline: none;
}
.todo-container {
  width: 600px;
  margin: auto;
  color: rgb(0, 0, 0);
}
.todo-container .todo-wrap {
  padding: 15px;
  border: 2px solid #000;
}
</style>
