<template>
  <div class="todo h-screen w-full" :class="mode">
    <div class="holder h-72"></div>

    <div id="todo-board" class="h-screen xl:w-1/2 lg:w-10/12 md:w-9/12 w-11/12 items-center">
      <div class="flex justify-between items-center">
        <h1 class="text-white text-xl tracking-widest">TODO</h1>
        <Theme :mode="mode" @nightmode="nightmode"/>
      </div>
    
      <form @submit.prevent="addTodo" action="" class="bg-gray-900 flex items-center md:gap-12 gap-5 shadow">
        <div class="undone"></div>
        <input type="text"
          placeholder="Create a new todo"
          v-model="newTodo"
          class="text-white py-3 focus:outline-none w-10/12">
      </form>

     <div class="todo-list bg-gray-900 shadow">

        <ul class="list-items">
          <li v-for="(todo, index) in filteredTodos" :key="todo.id" class="items">
            <div @click="toggleCompleted(todo)" :class="{'checked' : todo.completed}" class="undone">
              <img :class="{'iconchecked' : todo.completed}" class="w-auto pt-1 m-auto hidden" src="../assets/images/icon-check.svg" alt="">
            </div> 
              <p :class="{'namechecked' : todo.completed}" class="flex flex-col lg:ml-14 ml-5 w-10/12">{{ todo.name }}
              <span class="text-red-500 italic">{{ todo.date }}</span></p>

            <button class="deleteBtn butt"  @click="deleteTodo(index)"><img src="../assets/images/icon-cross.svg" alt=""></button>
          </li>
        </ul>
     </div>


      <div class="filterBtns bg-gray-900 lg:px-12 md:px-7 px-3 py-4 shadow ">
        <p class="sec1">{{ todos.length }} Items left</p>

        <div class="flex items-center gap-5">
          <button :class="{active: type ===''}" @click="filterType('')" class="butt">All</button>
          <button :class="{active: type ==='ongoing'}" @click="filterType('ongoing')" class="butt">Active</button>
          <button :class="{active: type ==='completed'}" @click="filterType('completed')" class="butt">Completed</button>
        </div>

        <button @click="clearCompleted" class="butt sec2">Clear Completed</button>
      </div>

      <div class="dnd text-white text-center mb-10 mt-10 sec3">
         <p>Drag and drop to reorder list</p>
      </div>



    </div>
  </div>
</template>

<script>

import Theme from '../components/Theme.vue'
export default {
  name: 'Todo',
  components: {
    Theme,
  },
  
  data() {
    return {
      
      mode: '',
      type: '',
      newTodo: '',
      todo: '',
      todos: []
    }
  },

  beforeMount() {

    this.newTodos = JSON.parse(localStorage.getItem('todos'))
    if (!this.newTodos) {
      fetch('./todos.json/') 
    .then(res => { return res.json()})
    .then(data => { localStorage['defaultTodo'] = JSON.stringify(data)
    this.todos = JSON.parse(localStorage.getItem('defaultTodo'))
    })
    } else {
        this.todos = this.newTodos
    }


    this.currentmode = localStorage.getItem('Theme')
    this.mode = this.currentmode
  },

  created() {
    setInterval(this.getNow, 1000)
  },

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
    saveTodo(todo) {
      if(!localStorage.getItem('todos')) {
        this.todos = []
      } else {
        this.todos = JSON.parse(localStorage.getItem('todos'))  
      }
       this.todos.unshift(this.todo)
      localStorage.setItem('todos', JSON.stringify(this.todos))

    },

    addTodo() {
      if(this.newTodo) {
        this.todo = {
          date: this.date,
          name: this.newTodo,
          completed: false
        }
        this.saveTodo() 
        this.newTodo = ''; 
        // alert('New task added successfully')
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
       localStorage.setItem('todos', JSON.stringify(this.todos))
    },

    clearCompleted() {
      this.todos = this.todos.filter((todo) => !todo.completed) 
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },

    nightmode() {
      this.mode === 'dark' ? this.mode = 'light' : this.mode = 'dark'
      localStorage.setItem('Theme', this.mode)
    },

    filterType(type) {
      this.type = type;
    },

    getNow: function() {
      const today = new Date();
      const date = today.getFullYear() + '-' + (today.getMonth() + 1) + '-' + today.getDate()
      this.date = date
    },


  }

 
}
</script>



<style>
.todo  {
  background: black;
  transition: background 0.5s ease-out;
}

 .dark {
   background: #fff;
   transition: background 0.5s ease-out;
 }

.dark .todo{
    background: #fff;
   color:#000;
   transition: background 0.5s ease-out;
}

.dark form{
    background: #fff;
   color:#000;
   transition: background 0.5s ease-out;
}

.dark input {
  color: #000;
}

.dark .todo-list{
  transition: background 0.5s ease-out;
    background: #fff;
   color:#000;
  box-shadow: var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow);	
}

.dark .dnd{
   color:#000;
}

.dark .items {
  border-bottom: 1px solid black;
  color: #000;
}

.dark .filterBtns{
    background: #fff;
    border-bottom: 1px solid black;
    border-top: 1px solid black;
    color:#000;
    transition: background 0.5s ease-out;
}

.holder{
  background-image:url('../assets/images/bg-desktop-dark.jpg');
  transition: background 0.5s ease-out;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
.dark .holder{
   background-image:url('../assets/images/bg-desktop-light.jpg');
   transition: background 0.5s ease-out;
}

</style>
