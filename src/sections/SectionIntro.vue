<script setup>
import IntroStart from './../parts/IntroStart.vue'
import IntroWords from './../parts/IntroWords.vue'
import IntroText from './../parts/IntroText.vue'
import IntroScroll from './../parts/IntroScroll.vue'
</script>

<template>
  <div id="burger-accueil" class="burger-orange">
    <div class="container">
      <IntroStart></IntroStart>
    </div>

    <div class="container">
      <IntroWords></IntroWords>
    </div>

    <div class="container-fluid">
      <IntroText></IntroText>
    </div>

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
</style>
