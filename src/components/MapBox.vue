<template>
  <MglMap
      :accessToken="accessToken"
      :mapStyle="mapStyle"
      :center="center"
      :zoom="zoom"
      container="myAwesomeMap"
  >
    <MglGeojsonLayer
        :sourceId="geoJsonSource.data.name"
        :source="geoJsonSource"
        layerId="myLayerId"
        :layer="geoJsonLayer"
    />
  </MglMap>
</template>

<script>
import { MglMap, MglGeojsonLayer } from "vue-mapbox";

export default {
  components: {
    MglMap,
    MglGeojsonLayer
  },
  props: {
    data: Object,
  },
  data: () => ({
    accessToken: 'pk.eyJ1IjoicmFkYXJ0cmlua2V0cyIsImEiOiJjazhyODV0YTIwN21wM2VwNjlyNjR4YmZ2In0.YY70N_F9VoD5-YRisQVojg', // your access token. Needed if you using Mapbox maps
    mapStyle: 'mapbox://styles/mapbox/outdoors-v11',
    // center: [125.6, 10.1],
    center: [41.9734, 45.0428],
    zoom: 6,
    geoJsonSource: {
      type: "geojson",
      data: {}
    },
    geoJsonLayer: {
      type: "circle",
      paint: {
        "circle-color": "#4264fb",
        'circle-radius': 8,
        'circle-stroke-width': 2,
        'circle-stroke-color': '#ffffff'
      }
    },
  }),
  mounted() {
    this.geoJsonSource.data = this.data;
  }
};
</script>

<style scoped>
</style>
