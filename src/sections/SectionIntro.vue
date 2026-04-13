<script setup>
import IntroStart from './../parts/IntroStart.vue'
import IntroWords from './../parts/IntroWords.vue'
import IntroText from './../parts/IntroText.vue'
import IntroScroll from './../parts/IntroScroll.vue'
import IntroMovingBg from './../parts/IntroMovingBg.vue'

import { onMounted, ref, inject } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const gsapContainers = ref([])

// timing values
const skipWordsDelay = 3000
const skipTextDelay = 15000
const tutorialDelay = 2000

const isMobile = window.innerWidth <= 576

// reactive state
let state = ref(1)
const introDiv = ref(null)
const html = document.documentElement
const isDev = ref(import.meta.env.DEV)
const setIntroDone = inject('setIntroDone')

function unlockScroll() {
  html.classList.remove('intro-active')
}

function HandleJumpToStats() {
  document.getElementById('burger-recapitulatif').scrollIntoView({ behavior: 'smooth' })
  setTimeout(() => {
    setIntroDone(true)
  }, 500)
  setTimeout(() => {
    ScrollTrigger.refresh()
    unlockScroll()
  }, 1500)
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

    if (isMobile) {
      setTimeout(() => {
        HandleJumpToStats()
      }, 2000)
    }

    setTimeout(() => {}, tutorialDelay)
  }, skipTextDelay + skipWordsDelay)
}

onMounted(() => {
  // En dev, on déverrouille immédiatement le scroll (la classe CSS intro-active est retirée)
  // En prod, le scroll reste verrouillé jusqu'à la fin de l'intro (géré via CSS .intro-active)
  // On n'écrit PLUS overflowY en JS au montage → évite le forced reflow
  if (isDev.value) {
    unlockScroll()
  }

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

  ScrollTrigger.create({
    trigger: introDiv.value,
    start: 'top bottom',
    onEnterBack: () => {
      state.value = 1
    },
  })
})
</script>

<template>
  <section id="burger-accueil" class="burger-orange" ref="introDiv">
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
  </section>
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
