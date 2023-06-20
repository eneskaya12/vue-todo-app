<template>
  <div>
    <div
      v-for="todo in todos"
      :key="todo.id"
      class="flex justify-between my-5 border-b-2 border-[#FFD95A] 2xl:w-1/2 mx-auto py-1 px-5"
    >
      <span
        :class="{
          'line-through text-gray-500': todo.done,
          'no-underline': !todo.done,
        }"
        class="text-3xl text-white font-['Dancing_Script']"
        >{{ todo.content }}</span
      >
      <div class="w-max h-max">
        <span
          @click="toggleDone(todo)"
          class="material-symbols-outlined cursor-pointer select-none text-3xl text-green-500 mr-5"
        >
          {{ todo.doneIcon }}
        </span>
        <span
          @click="deleteTodo(todo.id)"
          class="material-symbols-outlined cursor-pointer select-none text-3xl text-red-500"
        >
          delete
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoCard",
  props: {
    todos: Array,
  },
  methods: {
    deleteTodo(id) {
      this.$emit("delete-todo", id);
    },
    toggleDone(todo) {
      const updatedTodo = { ...todo };
      updatedTodo.done = !updatedTodo.done;
      updatedTodo.done ? (updatedTodo.doneIcon = "redo") : (updatedTodo.doneIcon = "done");
      this.$emit("toggle-done", updatedTodo);
    },
  },
};
</script>