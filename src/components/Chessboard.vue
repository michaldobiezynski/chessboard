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

<style scoped>
li {
  flex-basis: 12.5%;
}

li:nth-child(even).even {
  background: #779953;
}

li:nth-child(odd).odd {
  background: #779953;
}

li:nth-child(odd).even {
  background: #edeed1;
}

li:nth-child(even).odd {
  background: #edeed1;
}

.square {
  position: relative;
  list-style-type: none;
}

.clicked {
  position: absolute;
  background-color: #f7f769;
  width: 100%;
  height: 100%;
}

#chessboard-list {
  background-color: #333;
  display: flex;
  justify-content: stretch;
  align-items: stretch;
  width: min(60vw, 60vh);
  height: min(60vw, 60vh);
  flex-wrap: wrap;
  align-self: center;
  margin: 0;
  padding: 0;
  box-shadow: 0 8px 18px rgba(0, 0, 0, 0.25);
  border-radius: 4px;
  overflow: hidden;
}

@media only screen and (min-device-width: 280px) and (max-device-width: 600px) {
  #chessboard-list {
    width: min(70vw, 70vh);
    height: min(70vw, 70vh);
    margin: 8px;
  }
}
</style>
