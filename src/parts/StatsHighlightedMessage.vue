<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import gsap from 'gsap'
import messages from '@/data/highlighted-messages.json'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const currentIndex = ref(0)
const currentMessage = ref(messages[0])

onMounted(() => {
  const tl = gsap.timeline({ repeat: -1 })

  // État initial
  gsap.set('#stats-highlighted-quote', { x: -100, opacity: 0 })
  gsap.set('#stats-highlighted-date', { y: -30, opacity: 0 })
  gsap.set('#stats-highlighted-name', { y: 30, opacity: 0 })

  tl
    // Entrée
    .to('#stats-highlighted-quote', {
      x: 0,
      opacity: 1,
      duration: 0.6,
      ease: 'power2.out',
    })

    .to(
      '#stats-highlighted-date',
      {
        y: 0,
        opacity: 1,
        duration: 0.4,
      },
      '-=0.4',
    )

    .to(
      '#stats-highlighted-name',
      {
        y: 0,
        opacity: 1,
        duration: 0.4,
      },
      '-=0.4',
    )

    // Pause
    .to({}, { duration: 10 })

    // Sortie
    .to('#stats-highlighted-quote', {
      opacity: 0,
      duration: 0.4,
      ease: 'power1.in',
    })

    .to(
      '#stats-highlighted-date',
      {
        y: -30,
        opacity: 0,
        duration: 0.4,
      },
      '-=0.3',
    )

    .to(
      '#stats-highlighted-name',
      {
        y: 30,
        opacity: 0,
        duration: 0.4,
      },
      '-=0.3',
    )

    // Changement du texte
    .call(() => {
      currentIndex.value = (currentIndex.value + 1) % messages.length
      currentMessage.value = messages[currentIndex.value]
    })

    // Position avant nouveau message
    .set('#stats-highlighted-quote', { x: -100 })
    .set('#stats-highlighted-date', { y: -30 })
    .set('#stats-highlighted-name', { y: 30 })
})

// Apparition disparition
const section = ref(null)
let ctx

onMounted(() => {
  ctx = gsap.context(() => {
    const sentence = section.value.querySelector('#stats-highlighted-layout-message')
    const title = section.value.querySelector('#stats-highlighted-layout-title')

    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: section.value,
        start: 'center 80%',
        end: () => `+=${window.innerHeight * 0.6}`,
        toggleActions: 'play reverse play reverse',
      },
    })

    tl.from(title, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
    })

    tl.from(sentence, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
      delay: 0.2,
    })
  })
})

onBeforeUnmount(() => ctx?.revert())
</script>

<template>
  <div class="screen">
    <div ref="section">
      <div class="row">
        <div class="col-12">
          <div id="stats-highlighted-layout-title">
            <h2>Message mis en avant</h2>
          </div>
          <div id="stats-highlighted-layout-message">
            <div id="stats-highlighted-quote-block">
              <p class="stats-highlighted-informations" id="stats-highlighted-date">
                {{ currentMessage.date }}
              </p>
              <p id="stats-highlighted-quote">{{ currentMessage.message }}</p>
              <p class="stats-highlighted-informations" id="stats-highlighted-name">
                {{ currentMessage.name }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  display: flex;
  justify-content: center;
  align-items: center;
}

h2 {
  margin-bottom: 20px;
}

/* Style texte informations  */
.stats-highlighted-informations {
  font-family: arima, sans-serif;
  font-size: 23px;
  font-weight: 300;
  line-height: 23px;
}

/* Mise en page  */
#stats-highlighted-layout-message {
  display: flex;
  justify-content: center;
  align-items: center;
}

#stats-highlighted-quote-block {
  max-width: 637px;
  overflow: hidden;
}

#stats-highlighted-quote {
  font-family: arima, sans-serif;
  font-size: 24px;
  font-weight: 600;

  margin: 0 0 20px;
  transition: opacity 0.3s;
  line-height: 26px;
}

/* Position informations  */
#stats-highlighted-date {
  text-align: left;
}

#stats-highlighted-name {
  text-align: right;
}

@media (max-width: 768px) {
  .stats-highlighted-informations {
    font-family: arima, sans-serif;
    font-size: 21px;
    font-weight: 300;
    line-height: 21px;
    margin-bottom: 10px;
  }

  #stats-highlighted-quote {
    margin: 0 0 10px;
  }
}
</style>
