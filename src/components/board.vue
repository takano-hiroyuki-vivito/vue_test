<template>
  <div id="board">
    <div class="board-row">
      <cell :cellno="0" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
      <cell :cellno="1" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
      <cell :cellno="2" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
    </div>
    <div class="board-row">
      <cell :cellno="3" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
      <cell :cellno="4" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
      <cell :cellno="5" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
    </div>
    <div class="board-row">
      <cell :cellno="6" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
      <cell :cellno="7" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
      <cell :cellno="8" v-bind:cell-states="cellStates" v-on:cell-changed="boardClicked($event)"/>
    </div>
  </div>
</template>

<script>
import cell from "./cell.vue";

export default {
  name: "board",
  components: {
    cell
  },
  props: {
    cellno: Number,
    player: String,
    cellStates: Array
  },
  methods: {
    boardClicked: function(cellno) {
      this.$emit("cell-changed", cellno);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div.board-row {
  height: 31px;
  width: 93px;
  margin: auto;
}
</style>
