<template>
  <div class="todo">
    <div class="h-screen fixed">
      <img class="h-80" src="../assets/images/bg-desktop-dark.jpg" alt="">
      <div class="bg-black h-full"></div>
    </div>

    <div id="todo-board" class="w-1/2 items-center">
      <div class="flex justify-between items-center">
        <h1 class="text-white text-xl tracking-widest">TODO</h1>
        <img src="../assets/images/icon-sun.svg" alt="">
      </div>
    
      <form @submit.prevent="addTodo" action="" class="bg-gray-900 flex items-center gap-5">
        <!-- <input class="undone" v-model="undone"> -->
        <input type="text"
          placeholder="Create a new todo"
          v-model="newTodo"
          class="px-5 py-2 focus:outline-none text-white w-10/12">
      </form>

      <div class="bg-gray-900">

          <ul>
            <li v-for="todo in todos" :key="todo.id" class="items flex items-center gap-5">
              <span class="undone" :class="{completed : todo.completed}">{{ undone }}</span>
              <p :class="{completed : todo.completed}" @click="toggleCompleted(todo)">{{ todo.name }}</p> 
              <button id="deleteBtn" @click="deleteTodo(todo.id)"><img src="../assets/images/icon-cross.svg" alt=""></button>
            </li>
          </ul>
    
        <div class="flex items-center justify-between text-white px-12 py-5">
          <p>{{ todos.length }} Items left</p>

          <div class="flex items-center gap-5">
            <button @click="filterAll" class="butt focus:outline-none">All</button>
            <!-- <button @click="filterActive" class="butt focus:outline-none">Active</button> -->
            <button @click="filterCompleted" class="butt focus:outline-none">Completed</button>
          </div>

          <p>Clear Completed</p>
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
     undone: '',
     newTodo: '',
     todo: '',
     todos: []
    }
  },

  beforeMount: function() {
    if (this.todos) {
      this.todos = JSON.parse(localStorage.getItem('todos'))  
    } else 
      this.todos = []
  },


  computed: {
    // totalTodo: function() {
    //       if (!this.todos) {
    //           return 0;
    //       } else {
    //         todos.length
    //       }
    // }
  },


  methods: {
    saveTodo() {
      this.todos = JSON.parse(localStorage.getItem('todos'))  
      if(localStorage.getItem('todos') ===  null) {
        this.todos = []
      } else {
        this.todos = JSON.parse(localStorage.getItem('todos'))  
      }
       this.todos.push(this.todo)
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
  
    removeTodo(todo) {
      this.todos = JSON.parse(localStorage.getItem('todos'))

      this.todos.splice(todo.id, 1)

       localStorage.setItem('todos', JSON.stringify(this.todos))
    },

    addTodo() {
      if(this.newTodo) {
        this.todo = {
          id: this.todos.length + 1,
          name: this.newTodo,
          completed: false
        }
        this.saveTodo() 
        this.todos.push(this.todo)
        this.newTodo = ''; 
       } else {
          alert('No Task')
       }
       
    },

    toggleCompleted(todo) {
      todo.completed = !todo.completed;
    },

    deleteTodo(todo, id) {
       this.todos.splice(todo.id, 1)

       this.removeTodo(todo)
    },

    filterAll() {
      if(this.todos) {
       this.todos
      }
    },

    filterCompleted() {
      this.todos.forEach((todo) => {
        if (todo.completed) {
          this.todo
        }
      })
    },
  }
}
</script>



<style scoped>
  #todo-board {
    position: absolute;
    top: 100px;
    left: 350px;
  }
  form{
    padding: 5px 50px;
    margin: 40px 0;
  }
  input[type='text'] {
    background: transparent;
  }
 input[type='radio'] {
    background: transparent;
  }
  input :focus {
    outline: none;
  }
  .undone {
    width: 20px;
    height: 20px;
    border: 1px solid #808080;
    border-radius: 50%;
  }

  /* .done {
    width: 20px;
    height: 20px;
    border: 1px solid #808080;
    border-radius: 50%;
    background: url('../assets/images/icon-check.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-image: linear-gradient(to left, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
  } */

 .items {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    gap: 10px;
    font-size: 16px;
    padding: 30px 50px;
    color: white;
    border-bottom: 1px solid white;
  }

  .completed {
    text-decoration: line-through;
    opacity: 0.5;
    width: 20px;
    height: 20px;
    border: 1px solid #808080;
    border-radius: 50%;
    background: url('../assets/images/icon-check.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-image: linear-gradient(to left, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
}

.butt .active {
  color: blue
}

.butt a:focus {
  outline: none;
}

</style>
