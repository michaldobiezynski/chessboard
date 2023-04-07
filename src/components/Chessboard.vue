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
      squares: [], // An array to hold the square classes.
      selectedSquares: [], // An array to hold the selected squares.
      selectedSquare: -1, // Index of the currently selected square.
      numberOfClicks: 0, // Keeps track of the number of times squares have been clicked.
    };
  },

  methods: {
    // The onSquareClick method is called when a square is clicked.
    onSquareClick(index) {
      this.numberOfClicks++; // Increment the number of clicks.
      this.selectedSquare = index; // Set the selected square.
      this.selectedSquares.push(this.convertSquareToCordinate(index + 1)); // Push the selected square to the selectedSquares array.
      this.$emit("onSquareClick", this.selectedSquares); // Emit an event with the selectedSquares array.
    },

    // The convertSquareToCordinate method converts a square index to a coordinate string.
    convertSquareToCordinate(num) {
      const row = 8 - Math.floor((num - 1) / 8); // Calculate the row.
      const col = (num - 1) % 8; // Calculate the column.

      // Helper function to convert the column index to a letter.
      const convertColumnsToLetters = (col) => {
        const letters = ["a", "b", "c", "d", "e", "f", "g", "h"];
        return letters[col] || null;
      };

      return `${convertColumnsToLetters(col)}${row}`; // Return the coordinate string.
    },

    // The getSquareClasses method returns the classes for a given square.
    getSquareClasses(square, index) {
      let classes =
        square === "odd" ? `odd square ${index}` : `even square ${index}`;

      // Add classes to the top-left, top-right, bottom-left, and bottom-right squares.
      if (index === 0) classes += " top-left";
      if (index === 7) classes += " top-right";
      if (index === 56) classes += " bottom-left";
      if (index === 63) classes += " bottom-right";

      return classes;
    },
  },

  // The created method is called when the component is created.
  created() {
    let row = 1;
    // Create an array of squares.
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
/* Apply some basic styles to the list item */
li {
  flex-basis: 12.5%; /* Sets the flex-basis of each list item to 12.5% to ensure the chessboard layout remains consistent across different screen sizes. */
}

/* Alternate background colors for odd/even squares */

/* Set background color for even squares with even index */
li:nth-child(even).even {
  background: #779953;
}

/* Set background color for odd squares with odd index */
li:nth-child(odd).odd {
  background: #779953;
}

/* Set background color for even squares with odd index */
li:nth-child(odd).even {
  background: #edeed1;
}

/* Set background color for odd squares with even index */
li:nth-child(even).odd {
  background: #edeed1;
}

/* Style for each square */
.square {
  position: relative;
  list-style-type: none;
}

/* Highlight the clicked square with a yellow overlay */
.clicked {
  position: absolute;
  background-color: #f7f769;
  width: 100%;
  height: 100%;
}

/* Rounded corners for the top-left and top-right squares */
.top-left {
  border-top-left-radius: 4px;
}
.top-right {
  border-top-right-radius: 4px;
}

/* Rounded corners for the bottom-left and bottom-right squares */
.bottom-left {
  border-bottom-left-radius: 4px;
}
.bottom-right {
  border-bottom-right-radius: 4px;
}

/* Style for the chessboard list container */
#chessboard-list {
  background-color: #333;
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

/* Media query for smaller devices */
@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  /* Reduce the width and height of the chessboard list container */
  #chessboard-list {
    width: 80vw;
    height: 80vw;
    margin: 8px;
  }
}
</style>
