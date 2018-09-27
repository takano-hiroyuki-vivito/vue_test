<template>
  <div class="cell" v-on:click="handleClick">
    <button>
      {{ cellStates[cellno] }}
    </button>
  </div>
</template>

<script>
export default {
  name: "cell",
  props: {
    cellno: Number,
    cellStates: Array
  },
  methods: {
    handleClick: function() {
      // alert("clicked!"+this.cellno);
      if (this.cellStates[this.cellno] != "") {
        return;
      }

      this.$emit("cell-changed", this.cellno);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div.cell {
  border: solid 1px #666;
  height: 30px;
  width: 30px;
  margin: 0px -1px -1px 0px;
  float: left;
}
button{
        background-color: transparent;
        border: none;
        cursor: pointer;
        outline: none;
        padding: 0;
        appearance: none;
}
button {
  font-style: bold;
  font-size: 14pt;
}
</style>
