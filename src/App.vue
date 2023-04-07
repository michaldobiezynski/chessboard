<template>
  <div class="app">
    <div class="chessboard-wrapper">
      <chessboard @square-clicked="handleSquareClicked" />
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
    handleSquareClicked(square) {
      this.clickedSquares.push(square);
    },
  },
};
</script>
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
