<script setup>
import OutroAfterMovie from './../parts/OutroAfterMovie.vue'
import OutroMedia from './../parts/OutroMedia.vue'
import OutroInfo from './../parts/OutroInfo.vue'
import OutroScrollBg from './../parts/OutroScrollBg.vue'
</script>

<template>
  <div class="outro-container">
    <section id="burger-retour-image" class="burger-orange">
      <div class="container">
        <OutroAfterMovie></OutroAfterMovie>
      </div>
    </section>

    <div id="OutroZone">
      <OutroScrollBg></OutroScrollBg>
    </div>

    <section id="burger-informations" class="burger-blue">
      <div class="container-fluid">
        <OutroMedia></OutroMedia>
      </div>
      <div class="container">
        <OutroInfo></OutroInfo>
      </div>
    </section>
  </div>
</template>

<style scoped>
#OutroZone {
  position: absolute;
  inset: 0;
}

.outro-container {
  position: relative;
}

#burger-retour-image {
  position: relative;
  z-index: 1;
}
</style>
