<template>
  <div class="container">
    <Controls
      @input-change="setQuery"
      @toggle-sort="onToggleChanged"
    ></Controls>
    <div class="body">
      <Countries
        :query="query"
        @country-clicked="onCountryClicked"
        @selected-country-latlng="onCountryChanged"
        :sort="sort"
      ></Countries>
      <Map :test="test" :latlng="latlng" :markersLatLong="latlngs"></Map>
    </div>
  </div>
</template>

<script lang="ts">
import Map from "./components/Map.vue";
import Controls from "./components/Controls.vue";
import Countries from "./components/Countries.vue";
import { Component, Vue } from "vue-property-decorator";

export type Latlng = number[];

@Component({
  components: {
    Countries,
    Controls,
    Map
  }
})
export default class App extends Vue {
  private query = "";
  private latlng: Latlng = [];
  private sort = "One";
  private latlngs: Latlng[] = [];
  private test = "";

  public setQuery(payload: { message: string }): void {
    this.query = payload.message;
    console.log(payload.message);
  }
  public onCountryClicked(payload: { latlng: number[] }) {
    this.latlng = payload.latlng;
    //console.log("App", payload.latlng);
  }
  public onToggleChanged(payload: { sort: string }) {
    this.sort = payload.sort;
  }
  public onCountryChanged(payload: { latlngs: Latlng[] }) {
    //console.log("Ouncountrulist changed", payload.latlngs);
    this.latlngs = payload.latlngs;
    this.test += "a";
  }
}
</script>

<style>
ul {
  list-style-type: none;
}
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
}
</style>
