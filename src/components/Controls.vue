<template>
  <div class="controls">
    <h1>Controls</h1>
    <input v-model="message" @keydown="someHandler" placeholder="country" />
    <div>
      <h5>Sort By</h5>
      <input type="radio" id="one" value="One" v-model="picked" />
      <label for="one">Alphabet</label>
      <br />
      <input type="radio" id="two" value="Two" v-model="picked" />
      <label for="two">Population</label>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";

@Component
export default class Controls extends Vue {
  @Watch("picked")
  sortChanged(newVal: number[]) {
    // console.log(this.picked);
    this.$emit("toggle-sort", { sort: this.picked });
  }
  private message = "";
  private picked = "One";
  public someHandler() {
    this.$emit("input-change", { message: this.message });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
