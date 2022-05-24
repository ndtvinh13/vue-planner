<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">
      View All
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >
      Conpleted
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      On going
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],

  methods: {
    updateFilter(by) {
      this.$emit("filterChange", by);
      console.log(by);
    },
  },
};
</script>

<style>
.filter-nav button {
  display: inline-block;
  cursor: pointer;
  margin: 20px 10px 0 0;
  background: none;
  font-size: 15px;
  font-weight: bold;
  color: #bbb;
  text-transform: uppercase;
}

.filter-nav .active {
  color: #333;
}
</style>
