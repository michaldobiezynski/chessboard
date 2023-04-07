<template>
  <div class="sidebar">
    <h2>Clicked squares</h2>
    <div class="list-container">
      <ol class="scrollable-list">
        <li v-for="(square, index) in clickedSquares" :key="square + index">
          {{ square }}
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    clickedSquares: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
.sidebar {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  background-color: #e5e5e5;
  width: 100%;
  height: 100%;
}

h2 {
  margin-top: 0;
}

.list-container {
  flex-grow: 1;
  overflow-y: auto;
  margin-bottom: 2rem;
}

.scrollable-list {
  margin-left: 1.5rem;
  height: 100%;
}
</style>
