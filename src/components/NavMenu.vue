<template>
  <nav
      class="nav blue flex-column justify-space-between align-center pa-1"
      :style="isOpen ? 'width: 250px' : 'width: 50px'"
  >
    <v-btn v-show="isOpen" color="transparent" class="white--text">
      Осмотр
    </v-btn>
    <v-spacer></v-spacer>
    <v-btn @click="onMenuHandle" color="transparent" max-width="50px" min-width="50px" class="btn">
      <v-app-bar-nav-icon color="white" />
    </v-btn>
  </nav>
</template>

<script>
export default {
  data: () => ({
    isOpen: false,
  }),
  methods: {
    onMenuHandle() {
      this.isOpen = !this.isOpen;
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
