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
import ScrollToPlugin from 'gsap/ScrollToPlugin'

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin)

// onMounted(() => {
//   // bloque scroll au début
//   document.body.style.overflow = 'hidden'

//   const intro = document.querySelector('#intro-start')
//   const introWords = document.querySelector('#intro-words')

//   window.addEventListener('scroll', () => {
//     if (!hasStarted || isLocking) return
//     if (!intro) return

//     // empêche de remonter dans la cover
//     if (window.scrollY < window.innerHeight) {
//       isLocking = true

//       introWords.scrollIntoView({ behavior: 'smooth' })

//       setTimeout(() => {
//         isLocking = false
//       }, 50)
//     }
//   })
// })

// function unlockScroll() {
//   hasStarted = true
//   document.body.style.overflow = 'auto'
// }

// Frise
onMounted(() => {
  const mm = gsap.matchMedia()

  // DESKTOP DEUXIÈME TEST
  mm.add('(min-width: 993px)', () => {
    const timeline = document.querySelector('#timeline-container')
    const section = document.querySelector('main')

    // // hauteur de scroll de la section
    // const getSectionScroll = () => section.scrollHeight - window.innerHeight

    // // hauteur de scroll de la frise
    // const getTimelineScroll = () => timeline.scrollHeight - window.innerHeight

    // // sécurité : si la frise est plus petite → pas d’animation
    // if (getTimelineScroll() <= 0) return

    gsap.to(timeline, {
      y: () => -(timeline.scrollHeight - window.innerHeight),
      ease: 'none',
      scrollTrigger: {
        trigger: section,
        start: 'top top',
        end: 'bottom bottom',
        scrub: true,
        invalidateOnRefresh: true,
      },
    })

    // optionnel : gérer l'opacité en dehors de <main>
    ScrollTrigger.create({
      trigger: section,
      start: 'top top+=10%',
      end: 'bottom bottom-=10%',
      onEnter: () => gsap.set(timeline, { opacity: 1 }),
      onLeave: () => gsap.set(timeline, { opacity: 0 }),
      onEnterBack: () => gsap.set(timeline, { opacity: 1 }),
      onLeaveBack: () => gsap.set(timeline, { opacity: 0 }),
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

  <main id="main">
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
  display: flex;
  position: relative;
}

/* FRISE PREMIER TEST */
/* #timeline-container {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 10;
  pointer-events: none;
}

#timeline-container {
  height: auto;
} */

/* FRISE DEUXIEME TEST */
#timeline-container {
  position: fixed;
  top: 0;
  right: 0;
  width: 230px;
  z-index: 10;
  pointer-events: none;
  display: none;
}

/* FRISE MOBILE */
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
