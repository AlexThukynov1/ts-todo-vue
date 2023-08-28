<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        :key="filter"
        class="button"
        @click="setFilter(filter)"
        :class="{ 'button--primary': activeFilter === filter }"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>

<script lang="ts">
import { PropType, defineComponent } from "vue";
import { Filters } from "@/types/Filters";

interface State {
  filters: Filters[];
}

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<Filters>,
      required: true,
    },
  },
  data(): State {
    return {
      filters: ["All", "Active", "Done"],
    };
  },
  methods: {
    setFilter(filter: Filters) {
        this.$emit('setFilter', filter)
    }
  },
  emits: {
    setFilter: (filter: Filters) => filter
  }
});
</script>

<style scoped></style>
