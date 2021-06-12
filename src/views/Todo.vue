<template>
  <div class="todo">
    <img class="h-80" src="../assets/images/bg-desktop-dark.jpg" alt="">
    <div class="bg-black h-96">

      <div id="todo-board" class="w-1/2 items-center">
        <div class="flex justify-between items-center">
          <h1 class="text-white text-xl tracking-widest">TODO</h1>
          <img src="../assets/images/icon-sun.svg" alt="">
        </div>
      
        <form action="" class="bg-gray-900 flex items-center">
          <div class="undone"></div>
          <input type="text"
            placeholder="Create a new todo"
            v-model="task"
            class="px-5 py-2 focus:outline-none text-white" ?>
        </form>

        <div class="bg-gray-900">
          <ul>
            <li>{{ task }}</li>
          </ul>
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
      task: '',
      tasks: []
    }
  },

  methods: {

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

  li {
    font-size: 14px;
    padding: 15px;
    color: #fff;
    border-bottom: 1px solid white;
  }
</style>
