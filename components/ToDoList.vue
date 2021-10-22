<template>
<div>
  <ToDoItem
    v-for="(todo, index) in todos"
    :key="index"
    :todo="todo"
    @changeCheckbox="$emit('changeCheckbox', index)"
    @removeTodo="$emit('removeTodo', index)"
    @changeTitle="(title) =>
      $emit('changeTitle', {
        title,
        index,
      })
    "
  />
  </div>
</template>

<script >
export default {
  props: ["todos"],
};
</script>
