<template>
  <div class="hello"> 
     <div class="newTask">
       <input type="text" v-model="newTodo" name="" @keyup.enter="add">
     </div>
     <ol class="todos" v-cloak>
        <li v-for="item in todoList">
          <input type="checkbox" v-model="item.done">{{item.title}}
          <span v-if="item.done">已完成</span>
          <span v-else>未完成</span>
          <button @click="remove(item)">x</button>
        </li>
     </ol>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      newTodo: '',
      todoList: []
    }
  },
  methods: {
    add() {
      this.todoList.unshift({
        title: this.newTodo,
        time: new Date(),
        done: false
      })
      this.newTodo = ''
    },
    remove(todo){
      let index = this.todoList.indexOf(todo)
      this.todoList.splice(index, 1)
    }
  },
  created(){
    window.onbeforeunload = () => {
      let dataString = JSON.stringify(this.todoList) 
      window.localStorage.setItem('myTodos', dataString)
    }
      let oldDataString = window.localStorage.getItem('myTodos')
      let oldData = JSON.parse(oldDataString)
      this.todoList = oldData || []
      
  }
}
</script>

<style scoped>
[v-cloak] {
  display: none;
}
</style>
