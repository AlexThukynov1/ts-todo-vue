<template>
  <div id="app">
    <TdHeader />
    <TdFilters @set-filter="setFilter" :active-filter="activeFilter" />
    <main class="app-main">
      <TdTodoList
        :todos="filterTodo"
        @remove-todo="removeTodo"
        @togle-todo="togleTodo"
      />
      <TdAddTodo @add-todo="addTodo" />
    </main>
    <TdFooter :stats="stats" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TdAddTodo from "./components/TdAddTodo.vue";
import TdFilters from "./components/TdFilters.vue";
import TdFooter from "./components/TdFooter.vue";
import TdHeader from "./components/TdHeader.vue";
import TdTodoList from "./components/TdTodoList.vue";
import { Todo } from "@/types/Todo";
import { Filters } from "@/types/Filters";
import { Stats } from "@/types/Stats";

interface state {
  todos: Todo[];
  activeFilter: Filters;
}

export default defineComponent({
  name: "App",
  components: {
    TdHeader,
    TdFilters,
    TdTodoList,
    TdAddTodo,
    TdFooter,
  },
  data(): state {
    return {
      todos: [
        { id: 0, text: "Learn the basics of Vue", completed: true },
        { id: 1, text: "Learn the basics of Typescript", completed: false },
        { id: 2, text: "Subscribe to the channel", completed: false },
      ],
      activeFilter: "All",
    };
  },
  computed: {
    filterTodo(): Todo[] {
      switch (this.activeFilter) {
        case "Active":
          return this.todos.filter((todo) => !todo.completed);

        case "Done":
          return this.todos.filter((todo) => todo.completed);

        case "All":
        default:
          return this.todos;
      }
    },
    stats(): Stats {
      return {
        active: this.todos.filter((todo) => !todo.completed).length,
        done: this.todos.filter((todo) => todo.completed).length,
      };
    },
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.push(todo);
    },
    togleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id);

      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed;
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
    setFilter(filter: Filters) {
      this.activeFilter = filter;
    },
  },
});
</script>

<style>
@import url("../src//common/styles/main.css");
</style>
