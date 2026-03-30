<script setup>
import { ref, onMounted } from 'vue'
import gsap from 'gsap'
import messages from '@/data/highlighted-messages.json'

const currentIndex = ref(0)
const currentMessage = ref(messages[0])

onMounted(() => {
  const tl = gsap.timeline({ repeat: -1 })

  // État initial
  gsap.set('#quote', { x: -100, opacity: 0 })
  gsap.set('#date', { y: -30, opacity: 0 })
  gsap.set('#name', { y: 30, opacity: 0 })

  tl
    // Entrée
    .to('#quote', {
      x: 0,
      opacity: 1,
      duration: 0.6,
      ease: 'power2.out',
    })

    .to(
      '#date',
      {
        y: 0,
        opacity: 1,
        duration: 0.4,
      },
      '-=0.4',
    )

    .to(
      '#name',
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
    .to('#quote', {
      opacity: 0,
      duration: 0.4,
      ease: 'power1.in',
    })

    .to(
      '#date',
      {
        y: -30,
        opacity: 0,
        duration: 0.4,
      },
      '-=0.3',
    )

    .to(
      '#name',
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
    .set('#quote', { x: -100 })
    .set('#date', { y: -30 })
    .set('#name', { y: 30 })
})
</script>

<template>
  <div class="screen">
    <div>
      <h3>Message mis en avant</h3>
      <div class="row">
        <div class="col-12">
          <div id="layout-message">
            <div id="quote-block">
              <p class="informations" id="date">{{ currentMessage.date }}</p>
              <p id="quote">{{ currentMessage.message }}</p>
              <p class="informations" id="name">{{ currentMessage.name }}</p>
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

/* Style texte informations  */
.informations {
  font-family: arima, sans-serif;
  font-size: 23px;
  font-weight: 300;
  line-height: 23px;
}

/* Mise en page  */
#layout-message {
  display: flex;
  justify-content: center;
  align-items: center;
}

#quote-block {
  max-width: 637px;
  overflow: hidden;
}

#quote {
  font-family: arima, sans-serif;
  font-size: 24px;
  font-weight: 600;

  margin: 0 0 20px;
  transition: opacity 0.3s;
  line-height: 26px;
}

/* Position informations  */
#date {
  text-align: left;
}

#name {
  text-align: right;
}

@media (max-width: 768px) {
  .informations {
    font-family: arima, sans-serif;
    font-size: 21px;
    font-weight: 300;
    line-height: 21px;
    margin-bottom: 10px;
  }

  #quote {
    margin: 0 0 10px;
  }
}
</style>
