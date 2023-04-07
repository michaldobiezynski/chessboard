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

.top-left {
  border-top-left-radius: 4px;
}

.top-right {
  border-top-right-radius: 4px;
}

.bottom-left {
  border-bottom-left-radius: 4px;
}

.bottom-right {
  border-bottom-right-radius: 4px;
}

#chessboard-list {
  display: flex;
  justify-content: stretch;
  align-items: stretch;
  width: 40vw;
  height: 40vw;
  flex-wrap: wrap;
  align-self: center;
  margin: 20px;
  padding: 0;
  box-shadow: 0 8px 18px rgba(0, 0, 0, 0.25);
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  #chessboard-list {
    width: 95vw;
    height: 95vw;
    margin: 20px;
  }
}
</style>
