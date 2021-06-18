<template>
  <div class="todo">
    <div class="h-screen fixed">
      <img class="h-80" src="../assets/images/bg-desktop-dark.jpg" alt="">
      <div class="bg-black h-full"></div>
    </div>

    <div id="todo-board" class="lg:w-1/2 md:w-9/12 w-10/12 items-center">
      <div class="flex justify-between items-center">
        <h1 class="text-white text-xl tracking-widest">TODO</h1>
        <img src="../assets/images/icon-sun.svg" alt="">
      </div>
    
      <form @submit.prevent="addTodo" action="" class="bg-gray-900 flex items-center gap-10">
        <div class="undone"></div>
        <input type="text"
          placeholder="Create a new todo"
          v-model="newTodo"
          class="py-3 focus:outline-none text-white w-10/12">
      </form>

      <div class="todo-list bg-gray-900">

          <ul>
            <li v-for="(todo, index) in filteredTodos" :key="todo.id" class="items">
              <div @click="toggleCompleted(todo)" :class="{'checked' : todo.completed}" class="undone">
                <img :class="{'iconchecked' : todo.completed}" class="w-auto pt-1 m-auto hidden" src="../assets/images/icon-check.svg" alt=""></div> 
                <p :class="{'namechecked' : todo.completed}" class="ml-14 w-10/12">{{ todo.name }}</p>
                
              <button class="deleteBtn"  @click="deleteTodo(index)"><img src="../assets/images/icon-cross.svg" alt=""></button>
            </li>
          </ul>
    
        <div class="flex items-center justify-between text-white px-12 py-5">
          <p>{{ todos.length }} Items left</p>

          <div class="flex items-center gap-5">
            <button :class="{active: type ===''}" @click="filterType('')" class="butt focus:outline-none">All</button>
            <button :class="{active: type ==='ongoing'}" @click="filterType('ongoing')" class="butt focus:outline-none">Active</button>
            <button :class="{active: type ==='completed'}" @click="filterType('completed')" class="butt focus:outline-none">Completed</button>
          </div>

          <button @click="clearCompleted">Clear Completed</button>
        </div>
      </div>

    </div>
  </div>
</template>

<script>


export default {
  name: 'Todo',
  components: {
   
  },
  
  data() {
    return {
      type: '',
      newTodo: '',
      todo: '',
      todos: []
    }
  },

  // beforeMount: function() {
  //   if (this.todos) {
  //     this.todos = JSON.parse(localStorage.getItem('todos'))  
  //   } else 
  //     return false
  // },


  computed: {
    filteredTodos() {
      return this.todos.filter(todo => {
          switch(this.type) {
              case 'ongoing':
                  return !todo.completed;
              case 'completed':
                  return todo.completed;
              default:
                  return true;
          }
      });
  }
  },


  methods: {
    filterType(type) {
      this.type = type;
    },

    saveTodo(todo) {
      if(!localStorage.getItem('todos')) {
        this.todos = []
      } else {
        this.todos = JSON.parse(localStorage.getItem('todos'))  
      }
       this.todos.push(this.todo)
      localStorage.setItem('todos', JSON.stringify(this.todos))

    },
  
    removeTodo(index) {
      this.todos = JSON.parse(localStorage.getItem('todos'))
      this.todos.splice(index, 1)
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },

    addTodo() {
      if(this.newTodo) {
        this.todo = {
          // id: this.todos.length + 1,
          name: this.newTodo,
          completed: false
        }
        this.saveTodo() 
        this.newTodo = ''; 
       } else {
          alert('No Task')
       }
       
    },

    toggleCompleted(todo) {
      todo.completed = !todo.completed;     
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },

    deleteTodo(index) {
       this.todos.splice(index, 1)
       this.removeTodo(index)
    },

    clearCompleted() {
      this.todos.filter((todo) => this.todo.completed === true ? this.todos.remove(todo) : false)
    }

  }
}
</script>



<style scoped>
 

</style>
