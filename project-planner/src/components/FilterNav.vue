<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{active:current === 'all'}">All Project</button>
    <button @click="updateFilter('completed')" :class="{active:current === 'completed'}">Completed Project</button>
    <button @click="updateFilter('ongoing')" :class="{active:current === 'ongoing'}">Ongoing Project</button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    updateFilter(by) {
      this.$emit("filterChange", by);
    },
  },
};
</script>

<style>
    .filter-nav button {
        background: none;
        border: none;
        outline: none;
        color: #bbb;
        font-size: 15px;
        text-transform: uppercase;
        margin-right: 10px;
        letter-spacing: 1px;
        font-weight: bold;
        cursor: pointer;
    }
    .filter-nav button.active {
        color: #555;
    }
</style>
