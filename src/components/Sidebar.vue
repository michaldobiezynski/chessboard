<template>
  <div class="sidebar">
    <h2>Clicked squares</h2>
    <div class="list-container">
      <div class="list-wrapper">
        <div
          v-for="(square, index) in clickedSquares"
          :key="square + index"
          class="square"
        >
          {{ `${index + 1}. ` + square }}
        </div>
      </div>
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
  background-color: #3e3d39;
}

h2 {
  margin-top: 0;
  color: #fff;
  margin: 8px;
}

.list-container {
  flex-grow: 1;
  overflow-y: auto;
  height: min(50vw, 50vh);
  width: 100%;
}

.list-wrapper {
  display: flex;
  flex-wrap: wrap;
}

.square {
  color: #fff;
  padding: 1rem;
  background-color: #333;
  margin: 0.5rem;
  border-radius: 0.25rem;
}

.list-wrapper {
  flex-direction: column;
  overflow-x: hidden;
  overflow-y: auto;
  white-space: nowrap;
}

@media (min-width: 600px) {
  .list-container {
    height: 80vh;
  }
}
</style>
