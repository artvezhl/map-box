<template>
  <nav
      class="nav blue flex-column justify-space-between align-center pa-1"
      :style="isOpen ? 'width: 250px' : 'width: 50px'"
  >
    <v-btn v-show="isOpen" id="centerButton" @click="onButtonClick" color="transparent" class="white--text">
      Осмотр
    </v-btn>
    <v-spacer></v-spacer>
    <v-btn @click="onMenuHandle" color="transparent" max-width="50px" min-width="50px" class="btn">
      <v-app-bar-nav-icon color="white" />
    </v-btn>
  </nav>
</template>

<script>
import mapboxgl from "mapbox-gl";

export default {
  data: () => ({
    isOpen: false,
    data: null,
    coordinates: [],
    newCenter: [],
    newZoom: 0
  }),
  props: {
    currentMap: Object,
    geoData: Object
  },
  methods: {
    onMenuHandle() {
      this.isOpen = !this.isOpen;
    },
    newCenterFinder(firstCoord, lastCoord) {
      return [(firstCoord[0]+lastCoord[0])/2, (firstCoord[1]+lastCoord[1])/2];
    },
    // TODO refactor func to return zoom depends of destination between first and last points
    newZoomFinder(firstCoord, lastCoord){
      const latitude = lastCoord[1] - firstCoord[1];
      let zoom = 5;

      if (0.06 > latitude > 0.04) {
        zoom = 12;
      }

      return zoom;
    },
    onButtonClick() {
      const coordinates = this.geoData.data.features.map(feature => feature.geometry.coordinates);

      // Create a 'LngLatBounds' with both corners at the first coordinate.
      const bounds = new mapboxgl.LngLatBounds(
          coordinates[0],
          coordinates[0]
      );

      // Extend the 'LngLatBounds' to include every coordinate in the bounds result.
      for (const coord of coordinates) {
        bounds.extend(coord);
      }

      this.currentMap.fitBounds(bounds, {
        padding: 180
      });

      this.onMenuHandle();
    }
  }
}
</script>

<style scoped>
.nav {
  display: flex;
  position: absolute;
  top: 0;
  left: 0;
  height: 100vh;
  transition: ease .5s;
  z-index: 5;
}

.v-btn {
  z-index: 10;
  justify-self: flex-end;
}
</style>
