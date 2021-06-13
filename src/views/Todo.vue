<template>
  <div class="todo">
    <img class="h-80" src="../assets/images/bg-desktop-dark.jpg" alt="">
    <div class="bg-black h-screen">

      <div id="todo-board" class="w-1/2 items-center">
        <div class="flex justify-between items-center">
          <h1 class="text-white text-xl tracking-widest">TODO</h1>
          <img src="../assets/images/icon-sun.svg" alt="">
        </div>
      
        <form @submit.prevent="addTodo" action="" class="bg-gray-900 flex items-center">
          <div class="undone" v-model="undone"></div>
          <input type="text"
            placeholder="Create a new todo"
            v-model="newTodo"
            class="px-5 py-2 focus:outline-none text-white">
        </form>

        <div class="bg-gray-900 px-12 py-7">
          <div class="">
           <div class="items" v-for="todo in todos">
            <div class="undone">{{ undone }}</div>
            <p :class="{completed : todo.completed}" @click="toggleCompleted(todo)">{{ todo.name }}</p> 
            <button id="deleteBtn" @click="deletetodo(todo.id)"> X</button>
          </div>
          </div>

          <div class="flex items-center justify-between text-white">
            <p>0 items left</p>

            <div class="flex items-center gap-5">
              <p>All</p>
              <p>Active</p>
              <p>Completed</p>
            </div>

            <p>Clear Completed</p>
          </div>
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
     todos: []
    }
  },

  computed: {
    // filteredTodos() {
    //   return this.todo
    // }
  },

  methods: {
    addTodo() {
      this.todo = {
        id: this.todos.length + 1,
        name: this.newTodo,
        completed: false
       }
       this.todos.push(this.todo)
      this.newTodo = '';
      console.log(this.todos)
    }
  }
}
</script>

<style scoped>
  #todo-board {
    position: absolute;
    top: 150px;
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

  .done {
    width: 20px;
    height: 20px;
    border: 1px solid #808080;
    border-radius: 50%;
    background: url('../assets/images/icon-check.svg');
    background-repeat: no-repeat;
    background-position: center;
    background-image: linear-gradient(to left, hsl(192, 100%, 67%), hsl(280, 87%, 65%));
  }

 .items {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 10px;
    font-size: 16px;
    padding: 30px 15px;
    color: white;
    border-bottom: 1px solid white;
  }
</style>
