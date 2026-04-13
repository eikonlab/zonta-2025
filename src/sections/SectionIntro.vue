<script setup>
import IntroStart from './../parts/IntroStart.vue'
import IntroWords from './../parts/IntroWords.vue'
import IntroText from './../parts/IntroText.vue'
import IntroScroll from './../parts/IntroScroll.vue'
import IntroMovingBg from './../parts/IntroMovingBg.vue'

import { onMounted, ref, inject, watch } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const gsapContainers = ref([])

const isMobile = window.innerWidth <= 576

// reactive state
let state = ref(1)
const introDiv = ref(null)
const html = document.documentElement
const setIntroDone = inject('setIntroDone')
const isIntroDone = inject('isIntroDone')

function unlockScroll() {
  html.classList.remove('intro-active')
}

function lockScroll() {
  html.classList.add('intro-active')
}

function handleJumpToStats() {
  document.getElementById('burger-recapitulatif').scrollIntoView({ behavior: 'smooth' })
  setTimeout(() => {
    setIntroDone(true)
  }, 500)
  setTimeout(() => {
    ScrollTrigger.refresh()
    unlockScroll()
  }, 1500)
}

function handleStart() {
  window.scrollTo({
    top: window.innerHeight,
    behavior: 'smooth',
  })
  state.value = 2
}

const goToSecondSection = () => {
  window.scrollTo({
    top: window.innerHeight * 2,
    behavior: 'smooth',
  })

  state.value = 3
}

const goToThirdSection = () => {
  window.scrollTo({
    top: window.innerHeight * 3,
    behavior: 'smooth',
  })

  state.value = 4

  if (isMobile) {
    setTimeout(handleJumpToStats, 2000)
  }
}

onMounted(() => {
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
      window.scrollTo({
        top: 0,
        behavior: 'smooth',
      })

      setIntroDone(false)
      lockScroll()
      state.value = 1
    },
  })
})
</script>

<template>
  <section id="burger-accueil" class="burger-orange" ref="introDiv">
    <IntroMovingBg :state="state"></IntroMovingBg>

    <div class="container">
      <IntroStart @start="handleStart"></IntroStart>
    </div>

    <div class="container">
      <IntroWords :state="state" @nextSection="goToSecondSection"></IntroWords>
    </div>

    <div class="container-fluid gsap-container">
      <IntroText :state="state" @nextSection="goToThirdSection"></IntroText>
    </div>

    <div class="gsap-container">
      <div id="desktop-version">
        <IntroScroll :state="state" @jumpToStats="handleJumpToStats"></IntroScroll>
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
