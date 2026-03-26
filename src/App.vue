<script setup>
import PartOutro from './sections/SectionOutro.vue'
import PartIntro from './sections/SectionIntro.vue'
import PartStats from './sections/SectionStats.vue'
import BurgerMenu from './components/BurgerMenu.vue'

import Timeline from './components/Timeline.vue'
import TimelineMobile from './components/TimelineMobile.vue'

import { onMounted } from 'vue'
import gsap from 'gsap'

// FRISE
onMounted(() => {
  const timeline = document.querySelector('#timeline-container-mobile')
  const section = document.querySelector('main') // a section exacte où ça apparait

  // état initial : caché en bas
  gsap.set(timeline, { y: 50, opacity: 0 })

  const observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        // apparition depuis le bas
        gsap.to(timeline, {
          y: 0,
          opacity: 1,
          duration: 0.5,
          ease: 'power2.out',
        })
      } else {
        // disparition vers le bas
        gsap.to(timeline, {
          y: 50,
          opacity: 0,
          duration: 0.5,
          ease: 'power2.in',
        })
      }
    },
    { threshold: 0 }, // déclenche dès que la section touche le viewport
  )

  observer.observe(section)
})
</script>

<template>
  <BurgerMenu></BurgerMenu>

  <header>
    <PartIntro></PartIntro>
  </header>

  <main>
    <div id="timeline-container-mobile">
      <TimelineMobile></TimelineMobile>
    </div>

    <div id="timeline-container">
      <Timeline></Timeline>
    </div>

    <PartStats></PartStats>
  </main>

  <footer>
    <PartOutro></PartOutro>
  </footer>
</template>

<style scoped>
@media (max-width: 0px) {
  h1 {
    font-size: 30px;
  }
}

/* Frise */
main {
  position: relative;
}

#timeline-container {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 10;
  pointer-events: none;
  display: none;
}

#timeline-container-mobile {
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 10;
  pointer-events: none;
  display: none;
}
</style>
