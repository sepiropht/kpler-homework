<template>
  <div class="container">
    <Controls @input-change="setQuery"></Controls>
    <div class="body">
      <Countries :query="query" @country-clicked="onCountryClicked"></Countries>
      <Map :latlng="latlng"></Map>
    </div>
  </div>
</template>

<script lang="ts">
import Map from "./components/Map.vue";
import Controls from "./components/Controls.vue";
import Countries from "./components/Countries.vue";
import { Component, Vue } from "vue-property-decorator";

@Component({
  components: {
    Countries,
    Controls,
    Map,
  },
})
export default class App extends Vue {
  private query = "";
  private latlng: number[] = [];

  public setQuery(payload: { message: string }): void {
    this.query = payload.message;
    console.log(payload.message);
  }
  public onCountryClicked(payload: { latlng: number[] }) {
    this.latlng = payload.latlng;
    console.log("App", payload.latlng);
  }
}
</script>

<style>
.container {
  display: grid;
  grid-template-rows: 200px 1fr;
}

.controls {
  background-color: yellow;
}
.body {
  display: grid;
  grid-template-columns: 20% 1fr;
  min-height: 500px;
  max-height: 900px;
}

.country {
  background-color: red;
}

.map {
  background-color: green;
}
</style>
