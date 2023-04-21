<template>
  <div id="app">
    <div class="flex-container">
      <div class="flex-column chessboard-column">
        <div class="chessboard-wrapper">
          <chessboard @onSquareClick="handleSquareClicked" />
        </div>
      </div>
      <div class="flex-column sidebar-column">
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
  display: flex;
  place-items: center;
  justify-content: center;
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
}

.flex-column {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  height: 100%;
}

.chessboard-container {
  background-color: #504f4b;
}

.sidebar-container {
  background-color: #3e3d39;
}

.chessboard-wrapper {
  flex-grow: 1;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  .flex-container {
    flex-direction: column;
  }

  .chessboard-container {
    margin-top: 2rem;
    margin-bottom: 2rem;
  }
}

@media (min-width: 600px) {
  #app {
    flex-direction: row;
  }

  .chessboard-container {
    flex-basis: 0;
    flex-grow: 1;
    padding-bottom: 0;
  }

  .sidebar-container {
    flex-basis: 0;
    flex-grow: 1;
    margin-left: 2rem;
    margin-right: 2rem;
  }
}
</style>
