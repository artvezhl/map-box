<template>
  <v-app>
    <NavMenu />
    <v-main>
      <MapBox :data="geoData" />
    </v-main>
  </v-app>
</template>

<script>
import "mapbox-gl/dist/mapbox-gl.css";
import NavMenu from "@/components/NavMenu";
import MapBox from "@/components/MapBox";
import geoJsonData from "@/mock/index.js";

export default {
  name: 'App',
  components: {
    MapBox,
    NavMenu,
  },
  data: () => ({
    geoData: geoJsonData,
  }),
};
</script>

<style scoped>
#map {
  height: 100%;
}
</style>
