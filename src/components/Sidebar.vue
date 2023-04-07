<template>
  <div class="sidebar">
    <h2>Clicked squares</h2>
    <ol>
      <li v-for="(square, index) in clickedSquares" :key="square + index">
        {{ square }}
      </li>
    </ol>
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
  padding: 1rem;
  background-color: #e5e5e5;
  width: 100%;
}

h2 {
  margin-top: 0;
}

ol {
  padding-left: 1.5rem;
}
</style>
