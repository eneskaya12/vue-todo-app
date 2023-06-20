<template>
  <div id="app" class="bg-[#1B1A17] min-h-screen">
    <div class="container mx-auto flex justify-center flex-col items-center">
      <h1 class="mt-10 text-6xl text-[#FFD95A] font-['Dancing_Script']">
        Todo App
      </h1>
      <div class="mt-10 w-full">
        <form
          @submit.prevent="addTodo"
          class="flex justify-center flex-col 2xl:w-1/2 mx-auto"
        >
          <input
            v-model="todo"
            type="text"
            placeholder="Add todo"
            required
            class="w-full text-3xl text-white bg-transparent border-b-2 border-[#FFD95A] outline-none py-1 px-5 font-['Dancing_Script']"
          />
          <button type="submit" class="mt-10 w-max mx-auto">
            <span class="material-symbols-outlined text-5xl text-[#FFD95A]">
              add_circle
            </span>
          </button>
        </form>
        <div class="">
          <TodoCardVue :todos="todos" @delete-todo="deleteTodo" @toggle-done="toggleDone"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TodoCardVue from './components/TodoCard.vue';

export default {
  name: "App",

  data() {
    return {
      todo: "",
      todos: [],
      id: 1,
    };
  },
  watch: {
    todos: {
      handler() {
        localStorage.todos = JSON.stringify(this.todos);
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.todos) {
      this.todos = JSON.parse(localStorage.todos);
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        done: false,
        doneIcon: "done",
        content: this.todo,
        id: this.id++,
      });
      this.todo = "";
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    toggleDone(updatedTodo) {
      const index = this.todos.findIndex((todo) => todo.id === updatedTodo.id);
      if (index !== -1) {
        this.todos.splice(index, 1, updatedTodo);
      }
    },
  },

  components: {
    TodoCardVue
  },
};
</script>

<style>
</style>
