<template>
  <div v-if="isOpen" class="background">
    <div class="popup">
      <div>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nam, nesciunt quidem? Enim, incidunt minus neque
        nobis perspiciatis provident similique. Accusamus dolor ducimus maiores voluptate! Autem iste laudantium non
        odit provident.
      </div>
      <div>Earum eius eum excepturi fugiat illo illum iste laborum laudantium magni molestiae nihil, quae saepe unde ut
        voluptatibus. Amet corporis ducimus earum est excepturi iure laboriosam, provident repellat reprehenderit vel?
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isOpen: {
      type: Boolean,
      required: true
    }
  }
}
</script>

<style scoped>
.background {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, 0.5);
}
.popup {
  z-index: 10;
  width: 50%;
  background: white;
}
</style>
