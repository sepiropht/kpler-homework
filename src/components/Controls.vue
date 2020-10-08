<template>
  <div class="controls">
    <input
      class="search"
      v-model="message"
      @keyup="someHandler"
      placeholder="Search for country"
    />
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
  sortChanged(newVal: string) {
    // console.log(this.picked);
    this.$emit("toggle-sort", { sort: newVal });
  }
  private message = "";
  private picked = "One";
  public someHandler() {
    this.$emit("input-change", { message: this.message.trim() });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.controls {
  padding: 10px;
}
.search {
  padding: 10px;
  margin: 25px 0 0;
  border: 2px solid #eee;
  box-shadow: 0 0 15px 4px rgba(0, 0, 0, 0.06);
  border-radius: 10px;
  width: 80%;
}
</style>
