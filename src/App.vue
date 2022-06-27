<template>
  <v-app>
    <NavMenu :currentMap="map" :geoData="geoJsonSource" />
    <div id="map"></div>
  </v-app>
</template>

<script>
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";
import NavMenu from "@/components/NavMenu";
import geoJsonData from "@/mock/index.js";

export default {
  name: 'App',
  components: {
    NavMenu,
  },
  data: () => ({
    geoJsonSource: {
      type: "geojson",
      data: {}
    },
    geoJsonLayer: {
      id: "points",
      type: "circle",
      source: "points",
      paint: {
        "circle-color": "#4264fb",
        'circle-radius': 8,
        'circle-stroke-width': 2,
        'circle-stroke-color': '#ffffff'
      }
    },
    map: null
  }),
  mounted() {
    this.geoJsonSource.data = geoJsonData;
    mapboxgl.accessToken = 'pk.eyJ1IjoidmV6aGwiLCJhIjoiY2w0bzdhZnU2MDR1czNpazZ6NDBuanI0bSJ9.CKdDvxIFuVvVZJRIzezwGw';
    this.map = new mapboxgl.Map({
      container: 'map',
      style: 'mapbox://styles/mapbox/outdoors-v11',
      center: [46.9734, 45.0428],
      zoom: 6
    });
    this.map.on('load', () => {
      this.map.addSource('points', this.geoJsonSource);
      this.map.addLayer(this.geoJsonLayer);
    });
  }
};
</script>

<style scoped>
#map {
  height: 100%;
}
</style>
