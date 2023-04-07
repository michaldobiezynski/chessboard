<template>
    <div class="chessboard">
      <div
        v-for="(row, rowIndex) in 8"
        :key="rowIndex"
        class="chessboard-row"
      >
        <div
          v-for="(col, colIndex) in 8"
          :key="colIndex"
          :class="['chessboard-square', (rowIndex + colIndex) % 2 === 0 ? 'light' : 'dark']"
          @click="squareClicked(rowIndex, colIndex)"
        ></div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      squareClicked(rowIndex, colIndex) {
        this.$emit("square-clicked", { rowIndex, colIndex });
      },
    },
  };
  </script>
