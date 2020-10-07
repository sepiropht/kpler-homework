<template>
  <div class="map">
    <MglMap :accessToken="accessToken" :mapStyle="mapStyle" />
  </div>
</template>

<script>
import Mapbox from "mapbox-gl";
import { MglMap } from "vue-mapbox";

export default {
  components: {
    MglMap,
  },
  name: "Map",
  data() {
    return {
      accessToken:
        "pk.eyJ1Ijoic2VwaXJvcGh0IiwiYSI6ImNrMmdzaXZ5cTAzcDkzZG1seDdwN3R6aXgifQ.rvmMk75-5EUnz-YNQUmq6A", // your access token. Needed if you using Mapbox maps
      mapStyle: "mapbox://styles/mapbox/streets-v11", // your map style
    };
  },

  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map {
  height: 100% !important;
  width: 100% !important;
  position: relative;
}
MglMap {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
</style>
