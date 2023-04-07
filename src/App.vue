<template>
  <div id="app">
    <div class="flex-container">
      <div class="flex-column">
        <p>
          Click on a square to see the coordinates of the square in the sidebar.
        </p>
        <div class="chessboard-wrapper">
          <chessboard @onSquareClick="handleSquareClicked" />
        </div>
      </div>
      <div class="flex-column">
        <sidebar :clicked-squares="clickedSquares" />
      </div>
    </div>
  </div>
</template>

<script>
import Chessboard from "./components/Chessboard.vue";
import Sidebar from "./components/Sidebar.vue";

export default {
  components: {
    Chessboard,
    Sidebar,
  },
  data() {
    return {
      clickedSquares: [],
    };
  },
  methods: {
    handleSquareClicked(squares) {
      this.clickedSquares = squares;
    },
  },
};
</script>
<style>
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  font-family: "Arial", sans-serif;
  background-color: #504f4b;
}

p {
  color: #fff;
}

#app {
  display: flex;
  flex-direction: column;
  overflow: hidden;
  padding: 0;
}

.flex-container {
  display: flex;
  flex-grow: 1;
  height: 100%;
  width: 100%;
  background-color: #e0e0e0;
}

.flex-column {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  height: 100%;
  background-color: #504f4b;
}

.chessboard-wrapper {
  position: relative;
  flex-grow: 1;
  padding-bottom: 100%;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  .flex-container {
    flex-direction: column;
    justify-content: center;
  }
}

@media (min-width: 768px) {
  #app {
    flex-direction: row;
  }
  .chessboard-wrapper {
    flex-basis: 0;
    flex-grow: 1;
    padding-bottom: 0;
    height: 100%;
  }
}
</style>
