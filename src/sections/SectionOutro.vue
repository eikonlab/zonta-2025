<script setup>
import OutroAfterMovie from './../parts/OutroAfterMovie.vue'
import OutroMedia from './../parts/OutroMedia.vue'
import OutroInfo from './../parts/OutroInfo.vue'
</script>

<template>
  <div>
    <div id="burger-retour-image" class="burger-orange">
      <div class="container">
        <OutroAfterMovie></OutroAfterMovie>
      </div>
    </div>

    <div id="burger-informations" class="burger-blue">
      <div class="container">
        <OutroMedia></OutroMedia>

        <OutroInfo></OutroInfo>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
