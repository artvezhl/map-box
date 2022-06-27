<template>
  <v-app class="app_container">
    <NavMenu :currentMap="map" :openPopup="onPopupOpen" :moveToPopup="moveToPopup" :geoData="geoJsonSource" />
    <Popup :isOpen="isOpen" />
<!--    <MapPopup :currentMap="map"  />-->
    <div id="map"></div>
  </v-app>
</template>

<script>
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";
import NavMenu from "@/components/NavMenu";
import geoJsonData from "@/mock/index.js";
import Popup from "@/components/Popup";
import MapPopup from "@/components/MapPopup";

export default {
  name: 'App',
  components: {
    MapPopup,
    NavMenu,
    Popup
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
    map: null,
    isOpen: false
  }),
  methods: {
    onPopupOpen() {
      this.isOpen = true;
    },
    moveToPopup() {
      this.map.flyTo({
        center: [0, 0]
      })
    }
  },
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

    const coordinates = [0, 0];
    // create the popup
    const popup = new mapboxgl.Popup({ offset: 25 }).setText(
        'Construction on the Washington Monument began in 1848.'
    );

// create DOM element for the marker
    const el = document.createElement('div');
    el.id = 'marker';

// create the marker
    new mapboxgl.Marker(el)
        .setLngLat(coordinates)
        .setPopup(popup) // sets a popup on this marker
        .addTo(this.map);
  },

};
</script>

<style scoped>
#map {
  height: 100%;
}
.app_container {
  position: relative;
}
</style>
