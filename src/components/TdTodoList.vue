<template>
  <ul class="todo-list">
    <TdTodoItem
      v-for="todo in todos"
      :todo="todo"
      :key="todo.id"
      @togle-todo="togleTodo"
      @remove-todo="removeTodo"
    />
  </ul>
</template>

<script lang="ts">
import {PropType, defineComponent } from "vue";
import TdTodoItem from "./TdTodoItem.vue";
import { Todo } from "@/types/Todo";


export default defineComponent({
  components: {
    TdTodoItem,
  },
  props: {
    todos: {
        type: Array as PropType<Todo[]>
    }
  },
  methods: {
    togleTodo(id:number) {
        this.$emit('togleTodo', id)
    },
    removeTodo(id:number) {
        this.$emit('removeTodo', id)
    }
  },
  emits: {
    togleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  }

});
</script>

<style scoped></style>
