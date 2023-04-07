<template>
  <div class="sidebar">
    <h2>Clicked squares</h2>
    <div class="list-container">
      <ol>
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
  background-color: #3e3d39;
}

h2 {
  margin-top: 0;
  color: #fff;
}

li {
  color: #fff;
}

.list-container {
  flex-grow: 1;
  overflow-y: auto;
  margin-bottom: 2rem;
  height: 80vh;
  width: 100%;
}
</style>
