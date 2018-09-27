<template>
  <div id="app">
    <div>Now Player: {{ player }}</div>
    <div v-if="gameEnd">Finished!</div>
    <board v-bind:player="player" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
    <template v-for="step in result">
      <div  v-bind:key="step[0]">
        <button v-on:click="stepClicked(step[0])">
          Step: {{ step[0]+1 }}
        </button>
      </div>
    </template>
    <button v-on:click="resetGame">Reset</button>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import board from "./components/board.vue";

function judgeGameEnd(stateArray) {
  //yoko
  if (
    stateArray[0] != "" &&
    stateArray[1] != "" &&
    stateArray[2] != "" &&
    stateArray[0] === stateArray[1] &&
    stateArray[1] === stateArray[2]
  ) {
    return true;
  }
  if (
    stateArray[3] != "" &&
    stateArray[4] != "" &&
    stateArray[5] != "" &&
    stateArray[3] === stateArray[4] &&
    stateArray[4] === stateArray[5]
  ) {
    return true;
  }
  if (
    stateArray[6] != "" &&
    stateArray[7] != "" &&
    stateArray[8] != "" &&
    stateArray[6] === stateArray[7] &&
    stateArray[7] === stateArray[8]
  ) {
    return true;
  }
  //tate
  if (
    stateArray[0] != "" &&
    stateArray[3] != "" &&
    stateArray[6] != "" &&
    stateArray[0] === stateArray[3] &&
    stateArray[3] === stateArray[6]
  ) {
    return true;
  }
  if (
    stateArray[1] != "" &&
    stateArray[4] != "" &&
    stateArray[7] != "" &&
    stateArray[1] === stateArray[4] &&
    stateArray[4] === stateArray[7]
  ) {
    return true;
  }
  if (
    stateArray[2] != "" &&
    stateArray[5] != "" &&
    stateArray[8] != "" &&
    stateArray[2] === stateArray[5] &&
    stateArray[5] === stateArray[8]
  ) {
    return true;
  }
  //naname
  if (
    stateArray[0] != "" &&
    stateArray[4] != "" &&
    stateArray[8] != "" &&
    stateArray[0] === stateArray[4] &&
    stateArray[4] === stateArray[8]
  ) {
    return true;
  }
  if (
    stateArray[2] != "" &&
    stateArray[4] != "" &&
    stateArray[6] != "" &&
    stateArray[2] === stateArray[4] &&
    stateArray[4] === stateArray[6]
  ) {
    return true;
  }

  return false;
}

export default {
  name: "app",
  components: {
    board
  },
  data: function() {
    return {
      player: "O",
      cellStates: ["", "", "", "", "", "", "", "", ""],
      result: [],
      gameEnd: false,
      turn: 0
    };
  },
  methods: {
    boardClicked: function(cellno) {
      if (judgeGameEnd(this.cellStates)) {
        return;
      }
      if (this.turn < this.result.length) {
        let loopTimes = this.result.length - this.turn;
        for (let i = 0; i < loopTimes; i++) {
          this.result.pop();
        }
      }
      this.$set(this.cellStates, cellno, this.player);

      this.result.push([
        this.turn,
        this.cellStates.slice(0, this.cellStates.length)
      ]);
      this.turn = this.turn + 1;

      if (judgeGameEnd(this.cellStates)) {
        this.gameEnd = true;
        return;
      }
      if (this.player === "O") {
        this.player = "X";
      } else {
        this.player = "O";
      }
    },
    resetGame: function() {
      this.player = "O";
      this.cellStates = ["", "", "", "", "", "", "", "", ""];
      this.result = [];
      this.gameEnd = false;
      this.turn = 0;
    },
    stepClicked: function(step) {
      this.turn = this.result[step][0] + 1;
      this.cellStates = this.result[step][1];
      this.player = step % 2 == 0 ? "X" : "O";
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
