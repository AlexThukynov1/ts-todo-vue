<template>
  <li class="todo-item" :class="{'todo-item--done': todo.completed}" @click="togleTodo">
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTodo">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<script lang="ts">
import { PropType, defineComponent } from "vue";
import {Todo} from '@/types/Todo'

export default defineComponent({
  setup() {
    return {};
  },
  props: {
    todo: {
        type:Object as PropType<Todo>,
        required:true,
    }
},
methods: {
    togleTodo() {
        this.$emit('togleTodo', this.todo.id)
    },
    removeTodo() {
        this.$emit('removeTodo', this.todo.id)
    }
},
emits: {
    togleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
}
});
</script>

<style scoped></style>
