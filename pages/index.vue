<template>
  <div>
    <h1>ToDo List</h1>
    <input type="text" v-model="title" />
    <button @click="addtodo(title)">Add ToDo</button>
    <ToDoList
      :todos="todos"
      @changeCheckbox="changeCheckbox"
      @removeTodo="removeTodo"
      @changeTitle="changeTitle"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "@nuxtjs/composition-api";

export default defineComponent({
  setup() {
    const title = ref<string>("");
    const todos = ref<any>([]);

    const changeTitle = ({ index, title }: { index: number, title: string }) => {
      todos.value[index].title = title;
    };

    const changeCheckbox = (index: number) => {
      todos.value[index].completed = !todos.value[index].completed;
    };

    const addtodo = (todoTitle: string) => {
      todos.value.push({
        title: todoTitle,
        completed: false,
      });
      title.value = "";
    };

    const removeTodo = (index: number) => {
      todos.value.splice(index, 1);
    };

    return {
      changeTitle,
      changeCheckbox,
      addtodo,
      removeTodo,
      title,
      todos,
    };
  },
});
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