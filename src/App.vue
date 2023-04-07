<template>
  <!-- Main app container -->
  <div id="app">
    <!-- Flex container to arrange chessboard and sidebar columns -->
    <div class="flex-container">
      <!-- Column for chessboard -->
      <div class="flex-column chessboard-column">
        <!-- Chessboard component with click event handler -->
        <div class="chessboard-wrapper">
          <chessboard @onSquareClick="handleSquareClicked" />
        </div>
      </div>
      <!-- Column for sidebar -->
      <div class="flex-column sidebar-column">
        <!-- Sidebar component with clicked squares prop -->
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
      // Array to hold clicked square coordinates
      clickedSquares: [],
    };
  },
  methods: {
    // Click event handler for chessboard component
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

/* Global styling for paragraphs */
p {
  color: #fff;
}

/* Main app container */
#app {
  display: flex;
  flex-direction: column;
  overflow: hidden;
  padding: 0;
}

/* Flex container for chessboard and sidebar columns */
.flex-container {
  display: flex;
  flex-grow: 1;
  height: 100%;
  width: 100%;
}

/* Flex column for chessboard */
.flex-column {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  height: 100%;
}

/* Styling for chessboard container */
.chessboard-container {
  background-color: #504f4b;
}

/* Styling for sidebar container */
.sidebar-container {
  background-color: #3e3d39;
}

/* Styling for chessboard wrapper */
.chessboard-wrapper {
  flex-grow: 1;
}

/* Media queries for mobile devices */
@media only screen and (min-device-width: 320px) and (max-device-width: 768px) {
  /* Flex container to stack chessboard and sidebar columns */
  .flex-container {
    flex-direction: column;
  }

  /* Styling for chessboard container */
  .chessboard-container {
    margin-top: 2rem;
    margin-bottom: 2rem;
  }
}

/* Media queries for desktop devices */
@media (min-width: 768px) {
  /* Main app container */
  #app {
    flex-direction: row;
  }

  /* Styling for chessboard container */
  .chessboard-container {
    flex-basis: 0;
    flex-grow: 1;
    padding-bottom: 0;
  }

  /* Styling for sidebar container */
  .sidebar-container {
    flex-basis: 0;
    flex-grow: 1;
    margin-left: 2rem;
    margin-right: 2rem;
  }
}
</style>
