<script setup>
import IntroStart from './../parts/IntroStart.vue'
import IntroWords from './../parts/IntroWords.vue'
import IntroText from './../parts/IntroText.vue'
import IntroScroll from './../parts/IntroScroll.vue'
</script>

<template>
  <div id="burger-accueil" class="background-orange">
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
      <IntroScroll></IntroScroll>
    </div>
  </div>
</template>

<style scoped></style>
