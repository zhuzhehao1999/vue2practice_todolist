<template>
  <div class="todo-header">
    <input
      type="text"
      @keyup.enter="add()"
      v-model="title"
      placeholder="please input your task name, and click enter to add it"
    />
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
  name: "UserHeader",
  data() {
    return {
      //get the user input
      title:''
    };
  },
  methods:{
      add(){
          //check the data
          if(!this.title.trim()) return alert('input cannot be blank')
          //make the input become an object
          const todoObj = {id:nanoid(),title:this.title,done:false}
          //ask the App component to add a todo object
          this.addTodo(todoObj)
          //clean the input
          this.title='' 
      }
  },
  //get the props
  props:['addTodo']
};
</script>

<style scoped>
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(82, 168, 236, 0.6);
}
</style>