<script setup>
import IntroStart from './../parts/IntroStart.vue'
import IntroWords from './../parts/IntroWords.vue'
import IntroText from './../parts/IntroText.vue'
import IntroScroll from './../parts/IntroScroll.vue'
import IntroMovingBg from './../parts/IntroMovingBg.vue'

import { onMounted, ref } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const gsapContainers = ref([])

// timing values
const skipWordsDelay = 2000
const skipTextDelay = 2000
const tutorialDelay = 2000

const preventScroll = (e) => e.preventDefault()

// reactive state
let state = ref(1)
const introDiv = ref(null)
const html = document.documentElement

function HandleJumpToStats() {
  document.getElementById('burger-recapitulatif').scrollIntoView({ behavior: 'smooth' })
  setTimeout(() => {
    introDiv.value.style.display = 'none'
    window.scrollTo({
      top: 0,
      behavior: 'instant',
    })
  }, 1000)
  setTimeout(() => {
    html.style.overflowY = 'auto'
  }, 1500)
  console.log('Jump to stats section')
}

function HandleStart() {
  window.scrollTo({
    top: window.innerHeight,
    behavior: 'smooth',
  })
  state.value = 2

  setTimeout(() => {
    window.scrollTo({
      top: window.innerHeight * 2,
      behavior: 'smooth',
    })

    state.value = 3
  }, skipWordsDelay)

  setTimeout(() => {
    window.scrollTo({
      top: window.innerHeight * 3,
      behavior: 'smooth',
    })

    state.value = 4

    setTimeout(() => {}, tutorialDelay)
  }, skipTextDelay + skipWordsDelay)
}

onMounted(() => {
  html.style.overflowY = 'hidden'

  gsapContainers.value = document.querySelectorAll('.gsap-container')

  gsapContainers.value.forEach((container) => {
    gsap.set(container, {
      opacity: 0,
    })

    gsap.to(container, {
      opacity: 1,
      delay: 0.5,
      duration: 1,
      ease: 'power2.out',
      scrollTrigger: {
        trigger: container,
        start: 'top 80%',
        end: 'top 30%',
      },
    })
  })
})
</script>

<template>
  <div id="burger-accueil" class="burger-orange" ref="introDiv">
    <IntroMovingBg :state="state"></IntroMovingBg>

    <div class="container">
      <IntroStart @start="HandleStart"></IntroStart>
    </div>

    <div class="container">
      <IntroWords :state="state"></IntroWords>
    </div>

    <div class="container-fluid gsap-container">
      <IntroText></IntroText>
    </div>

    <div class="gsap-container">
      <div id="desktop-version">
        <IntroScroll @jumpToStats="HandleJumpToStats"></IntroScroll>
      </div>
    </div>
  </div>
</template>

<style scoped>
#desktop-version {
  height: 100vh;
  padding: 0;
  margin: 0;
  width: 100%;
}

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
