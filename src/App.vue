<script setup>
import PartOutro from './sections/SectionOutro.vue'
import PartIntro from './sections/SectionIntro.vue'
import PartStats from './sections/SectionStats.vue'
import BurgerMenu from './components/BurgerMenu.vue'

import Timeline from './components/Timeline.vue'
import TimelineMobile from './components/TimelineMobile.vue'

import { onMounted } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  const mm = gsap.matchMedia()

  // DESKTOP
  mm.add('(min-width: 993px)', () => {
    const timeline = document.querySelector('#timeline-container')
    const section = document.querySelector('main')

    gsap.set(timeline, { x: 80, opacity: 0, y: 0 })

    gsap
      .timeline({
        scrollTrigger: {
          trigger: section,
          start: 'top top',
          end: 'bottom bottom',
          scrub: 1,
        },
      })
      .to(timeline, {
        x: 0,
        opacity: 1,
        ease: 'power2.out',
        duration: 0.2,
      })
      .to(timeline, {
        y: () => -(timeline.scrollHeight - window.innerHeight),
        ease: 'none',
        duration: 1,
      })
      .to(timeline, {
        x: 0,
        opacity: 0,
        ease: 'power2.in',
        duration: 0.2,
      })
  })

  // MOBILE
  mm.add('(max-width: 992px)', () => {
    const timeline = document.querySelector('#timeline-container-mobile')
    const section = document.querySelector('main')

    gsap.set(timeline, { y: 50, opacity: 0, x: 0 })

    ScrollTrigger.create({
      trigger: section,
      start: 'top bottom',
      end: 'bottom bottom',
      onEnter: () => {
        gsap.to(timeline, { y: 0, opacity: 1, duration: 0.5 })
      },
      onLeave: () => {
        gsap.to(timeline, { y: 50, opacity: 0, duration: 0.5 })
      },
      onEnterBack: () => {
        gsap.to(timeline, { y: 0, opacity: 1, duration: 0.5 })
      },
      onLeaveBack: () => {
        gsap.to(timeline, { y: 50, opacity: 0, duration: 0.5 })
      },
    })

    const children = Array.from(timeline.children)

    gsap.to(children, {
      x: () => -(timeline.scrollWidth - window.innerWidth),
      ease: 'none',
      stagger: 0.1,
      scrollTrigger: {
        trigger: section,
        start: 'top bottom',
        end: 'bottom top',
        scrub: true,
      },
    })
  })
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
/* Frise */
main {
  position: relative;
}

#timeline-container {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 10;
  pointer-events: none;
  overflow: hidden;
}

#timeline-container-mobile {
  position: fixed;
  bottom: 0;
  left: 0;
  z-index: 10;
  pointer-events: none;

  display: none;
  opacity: 0;
  overflow: hidden;
}

@media (max-width: 992px) {
  #timeline-container-mobile {
    display: block;
    opacity: 1;
  }

  #timeline-container {
    display: none;
    opacity: 0;
  }
}
</style>
