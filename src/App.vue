<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './conponents/TodoHeader.vue'
import TodoInput from './conponents/TodoInput.vue'
import TodoList from './conponents/TodoList.vue'
import TodoFooter from './conponents/TodoFooter.vue'

export default {
  data(){
    return{
      todoItems:[]
    }
  },
  created(){
    if(localStorage.length>0){
        for(var i = 0; i< localStorage.length; i++){
            this.todoItems.push(localStorage.key(i));
        }
    }
  },
  methods:{
    clearAll(){
      localStorage.clear();
      this.todoItems = [];
    },
    addTodo(todoItem){
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    removeTodo(todoItem, index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    }

},
  components:{
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}
</script>

<style>
body{
    text-align: center;
    background-color: #f6f6f6;
}
input{
    border-style: groove;
    width: 200px;
}
button{
    border-style: groove;
}
.shadow{
    box-shadow: 5px, 10px, 10px, rgba(0,0,0,0.03);
}
</style>
