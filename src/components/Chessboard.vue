<template>
  <ul id="chessboard-list">
    <li
      v-for="(square, index) of squares"
      v-bind:key="index"
      v-bind:class="getSquareClasses(square, index)"
      @click="onSquareClick(index)"
    >
      <div v-if="selectedSquare === index" class="clicked" />
    </li>
  </ul>
</template>

<script>
export default {
  name: "Chessboard",
  data() {
    return {
      squares: [],
      selectedSquares: [],
      selectedSquare: -1,
      numberOfClicks: 0,
    };
  },

  methods: {
    onSquareClick(index) {
      this.numberOfClicks++;
      this.selectedSquare = index;
      this.selectedSquares.push(this.convertSquareToCordinate(index + 1));
      this.$emit("onSquareClick", this.selectedSquares);
    },

    convertSquareToCordinate(num) {
      const row = 8 - Math.floor((num - 1) / 8);
      const col = (num - 1) % 8;

      const convertColumnsToLetters = (col) => {
        const letters = ["a", "b", "c", "d", "e", "f", "g", "h"];
        return letters[col] || null;
      };

      return `${convertColumnsToLetters(col)}${row}`;
    },

    getSquareClasses(square, index) {
      let classes =
        square === "odd" ? `odd square ${index}` : `even square ${index}`;

      if (index === 0) classes += " top-left";
      if (index === 7) classes += " top-right";
      if (index === 56) classes += " bottom-left";
      if (index === 63) classes += " bottom-right";

      return classes;
    },
  },

  created() {
    let row = 1;
    [...Array(64)].forEach((_, i) => {
      if (i % 8 === 0) row = row + 1;

      if (row % 2 === 0) {
        this.squares.push("even");
      } else {
        this.squares.push("odd");
      }
    });
  },
};
</script>
