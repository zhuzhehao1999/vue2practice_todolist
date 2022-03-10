<template>
  <li>
      <label>
          <input type="checkbox" :checked="todo.doen" @change="handleCheck(todo.id)">
          <!-- follow code can do, but it deny the rule of props -->
          <!-- <input type="checkbox" v-model="todo.done"/> -->
          <span style="margin-left:10px">{{todo.title}}</span>
      </label>
      <button class="btn btn-danger" @click="handleDelete(todo.id)">Delete</button>
  </li>
</template>

<script>
export default {
    name:"UserItem",
    props:['todo','checkTodo','DeleteTodo'],
    methods:{
        // check or uncheck
        handleCheck(id){
            this.checkTodo(id)
        },
        //delete
        handleDelete(id){
            if(confirm('Delete?')){
                //ask App component to delete todo Object
                this.deleteTodo(id)
            }
        }
    }
}
</script>

<style scoped>
	li {
		list-style: none;
		height: 36px;
		line-height: 36px;
        color:rgb(0, 255, 0);
		padding: 0 5px;
		border-bottom: 1px solid #ddd;
	}

	li label {
		float: left;
		cursor: pointer;
	}

	li label li input {
		vertical-align: middle;
		margin-right: 6px;
		position: relative;
		top: -1px;
	}

	li button {
		float: right;
		display: none;
		margin-top: 3px;
	}

	li:before {
		content: initial;
	}

	li:last-child {
		border-bottom: none;
	}

	li:hover{
		background-color: #ddd;
	}
	
	li:hover button{
		display: block;
	}
</style>