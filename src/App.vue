<template>
  <div class="flex justify-center flex-col">
    <div class="text-3xl m-6">TODO APP</div>
    <div v-if="show" class="flex justify-center m-4">
      <div>
        <h3 class="text-3xl text-yellow-500">Update Area</h3>
        <input v-model="item.text" type="text" class="text-2xl rounded-full border-2 border-yellow-400 w-full h-12 p-2">
      </div>

      <button class="bg-red-300 hover:bg-red-600 hover:shadow-xl flex flex-row text-center text-3xl p-4 m-4" @click="changeTodo">change</button>
    </div>
    <div class="flex justify-center">
      <div class="w-1/2">
         <input
        v-model="todo"
        type="text"
        class="text-4xl rounded-full border-2 border-black w-full h-24 p-2"
      />
      <div class="flex flex-col align-center content-center w-full">
      <div v-for="todo in todos" :key="todo.id" class="flex flex-row justify-between w-full ">
        <div class="flex flex-col text-3xl items-start justify-center  p-4 w-full  ">
          {{ todo.text }}
        </div>
        <div class="items-center justify-items-end flex">
          <button
            class="bg-red-300 hover:bg-red-600 hover:shadow-xl flex flex-row text-3xl p-4 m-4 justify-end "
            @click="remove(todo.id)"
          >
            X
          </button>
          <button
            class="bg-blue-300 hover:bg-blue-600 hover:shadow-xl flex flex-row text-3xl p-4 m-4 justify-end "
            @click="updateTodo(todo)"
          >
            Edit
          </button>
        </div>
      </div>
    </div>
      </div>
     <div class=" flex-col flex">
       <button
        class="bg-gradient-to-r bg-green-200 hover:from-green-800  hover:to-green-500 hover:shadow-xl rounded-full text-3xl m-4 p-4"
        @click="addTodo"
      >
        Add Todo
      </button>
      <button
        class="bg-gradient-to-r bg-red-300 hover:from-red-900  hover:to-red-500 hover:shadow-xl rounded-full text-3xl m-4 p-4"
        @click="clearTodo "
      >
        Clear All Todo
      </button>
     </div>
      
    </div>

  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      todo: "",
      show: false,
      item: {
        id: '',
        text: ''
      },
      todos: [
        {id:1, text:'play game'},
        {id:2, text:'walking'},
      ],
    };
  },
  methods: {
    changeTodo() {
      const td = this.todos.find(i => i.id === this.item.id)
      td.text = this.item.text
      this.show = false
    },
    updateTodo(todo){
      this.show = true
      this.item = {
        id: todo.id,
        text: todo.text
      }
    },
    addTodo() {
      if (this.todo.length === 0) {
        return;
      }
      this.todos.push({
        id: Math.random(),
        text: this.todo,
      });
      this.todo = "";
    },
    remove(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
    },
    clearTodo(){
      this.todos = []
    },
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
