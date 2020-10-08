<template>
  <div id="mapContainer" class="map"></div>
</template>

<script lang="ts">
import Mapbox, { Marker } from "mapbox-gl";
import { Component, Prop, Vue, Watch } from "vue-property-decorator";
import { Latlng } from "../App.vue";
@Component
export default class Map extends Vue {
  @Prop([]) latlng: number[] = [];
  @Prop([]) markersLatLong: Latlng[] = [];
  @Prop(String) test = "";

  private markers: Marker[] = [];
  @Watch("latlng")
  async latlngChanged(newVal: number[]) {
    this.latlng = newVal;
    const [lat, lon] = newVal;
    this.map
      ? this.map.flyTo({
          center: [lon, lat],
          zoom: 3,
          speed: 2
        })
      : "";
  }
  @Watch("test")
  latlngsChanged() {
    this.markers.forEach(marker => marker.remove());
    this.markersLatLong.forEach(([lat, lon]) => {
      this.map
        ? this.markers.push(new Marker().setLngLat([lon, lat]).addTo(this.map))
        : "";
    });
  }
  private accessToken =
    "pk.eyJ1Ijoic2VwaXJvcGh0IiwiYSI6ImNrMmdzaXZ5cTAzcDkzZG1seDdwN3R6aXgifQ.rvmMk75-5EUnz-YNQUmq6A"; // your access token. Needed if you using Mapbox maps
  private mapStyle = "mapbox://styles/mapbox/streets-v11"; // your map style
  private map?: Mapbox.Map = undefined;

  mounted() {
    Mapbox.accessToken = this.accessToken;

    this.map = new Mapbox.Map({
      container: "mapContainer",
      style: this.mapStyle,
      center: [0, 0],
      zoom: 2
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map {
  height: 100%;
  width: 100%;
}
</style>
