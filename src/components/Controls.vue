<template>
  <div class="controls">
    <h1>Controls</h1>
    <input v-model="message" @keydown="someHandler" placeholder="country" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Controls extends Vue {
  private message = "";
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
