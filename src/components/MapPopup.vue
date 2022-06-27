<template>
  <div id="map"></div>
</template>

<script>
export default {
  props: {
    currentMap: Object,
  },
  data: () => {
    map: null
  },
  mounted() {
    this.map = this.currentMap;
  },
  methods: {
    setPopup() {
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
    }
  }
}
</script>

<style scope>
#marker {
  background-image: url('https://docs.mapbox.com/mapbox-gl-js/assets/washington-monument.jpg');
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}

.mapboxgl-popup {
  max-width: 200px;
}
</style>
