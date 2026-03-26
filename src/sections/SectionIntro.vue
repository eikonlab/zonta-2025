<script setup>
import IntroStart from './../parts/IntroStart.vue'
import IntroWords from './../parts/IntroWords.vue'
import IntroText from './../parts/IntroText.vue'
import IntroScroll from './../parts/IntroScroll.vue'
import IntroMovingBg from './../parts/IntroMovingBg.vue'

// ACCUEIL BLOQUÉ
defineEmits(['start'])
</script>

<template>
  <div id="burger-accueil" class="burger-orange">
    <div class="container">
      <IntroStart @start="$emit('start')"></IntroStart>
    </div>

    <div class="container">
      <IntroWords></IntroWords>
    </div>

    <div class="container-fluid">
      <IntroText></IntroText>
    </div>

    <IntroMovingBg></IntroMovingBg>

    <div class="container">
      <div id="desktop-version">
        <IntroScroll></IntroScroll>
      </div>
    </div>
  </div>
</template>

<style scoped>
@media (max-width: 576px) {
  #desktop-version {
    display: none;
    pointer-events: none;
  }
}

.burger-orange {
  position: relative;
}
</style>
