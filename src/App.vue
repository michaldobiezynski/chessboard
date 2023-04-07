<template>
  <div class="app">
    <div class="chessboard-wrapper">
      <chessboard @onSquareClick="handleSquareClicked" />
    </div>
    <sidebar :clicked-squares="clickedSquares" />
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
body,
#app {
  margin: 0;
  padding: 0;
  height: 100%;
  font-family: "Arial", sans-serif;
}

.app {
  display: flex;
  flex-direction: column;
  height: 100%;
  overflow: hidden;
}

.chessboard-wrapper {
  position: relative;
  flex-grow: 1;
  padding-bottom: 100%;
}

@media (min-width: 768px) {
  .app {
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
