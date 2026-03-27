<script setup>
import IntroStart from './../parts/IntroStart.vue'
import IntroWords from './../parts/IntroWords.vue'
import IntroText from './../parts/IntroText.vue'
import IntroScroll from './../parts/IntroScroll.vue'
import IntroMovingBg from './../parts/IntroMovingBg.vue'

import { onMounted } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

// timing values
const skipWordsDelay = 3000
const skipTextDelay = 5000
const tutorialDelay = 2000

function HandleStart() {
  window.scrollTo({
    top: window.innerHeight,
    behavior: 'smooth',
  })

  setTimeout(() => {
    // hasStarted = true
    window.scrollTo({
      top: window.innerHeight * 2,
      behavior: 'smooth',
    })
  }, skipWordsDelay)

  setTimeout(() => {
    // hasStarted = true
    window.scrollTo({
      top: window.innerHeight * 3,
      behavior: 'smooth',
    })

    setTimeout(() => {
      window.addEventListener('wheel', (e) => e, { passive: false })
    }, tutorialDelay)
  }, skipTextDelay + skipWordsDelay)
}

onMounted(() => {
  // bloque scroll au début
  // window.addEventListener('wheel', (e) => e.preventDefault(), { passive: false })
})
</script>

<template>
  <div id="burger-accueil" class="burger-orange">
    <IntroMovingBg></IntroMovingBg>

    <div class="container">
      <IntroStart @start="HandleStart"></IntroStart>
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

.burger-orange {
  position: relative;
}
</style>
