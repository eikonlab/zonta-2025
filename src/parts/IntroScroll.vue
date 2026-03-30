<script setup>
import ButtonScroll from './../components/ButtonScroll.vue'
</script>

<template>
  <div class="screen" id="intro-scroll">
    <div id="position-button-scroll">
      <ButtonScroll></ButtonScroll>
    </div>
  </div>
</template>

<style scoped>
.screen {
  position: relative;
}

@media (max-width: 992px) {
  .screen {
    height: 500px;
  }
}

/* Position bouton scroll */

#position-button-scroll {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: 0;
}
</style>
