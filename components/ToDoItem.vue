<template>
  <ul>
    <li>
      <input
        type="checkbox"
        @click="$emit('changeCheckbox')"
        v-model="todo.completed"
      />
      <span v-show="!hide" :class="{ checkbox: todo.completed }">{{
        todo.title
      }}</span>
      <input v-show="hide" type="text" v-model="todo.title" />
      <button @click="titleEdit">{{ hide ? "Save" : "Edit" }}</button>
      <button @click="$emit('removeTodo')">x</button>
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent, ref } from "@nuxtjs/composition-api";

export default defineComponent({
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  setup({ todo }: any, { emit }) {
    const hide = ref<Boolean>(false);

    const titleEdit = () => {
      hide.value = !hide.value;
      if (hide) {
        return;
      }
      emit("changeTitle", todo.title);
    };

    return {
      hide,
      titleEdit,
    };
  },
});
</script>

<style scoped>
.checkbox {
  text-decoration-line: line-through;
}

li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 3px;
  width: 500px;
  margin: 0 auto;
}
</style>