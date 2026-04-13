<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const props = defineProps({ state: Number })
const section = ref(null)
let ctx
defineEmits(['nextSection'])

onMounted(() => {
  const sentenceTop = section.value.querySelector('#intro-text-sentence-top')
  const sentenceBottom = section.value.querySelector('#intro-text-sentence-bottom')
  const image = section.value.querySelector('#intro-text-img')

  ctx = gsap.context(() => {
    const mm = gsap.matchMedia()

    // Desktop : ScrollTrigger classique
    mm.add('(min-width: 577px)', () => {
      const tl = gsap.timeline({
        scrollTrigger: {
          trigger: section.value,
          start: 'center 80%',
          end: () => `+=${window.innerHeight * 0.6}`,
          toggleActions: 'play reverse play reverse',
        },
      })
      tl.from(image, { opacity: 0, x: 70, duration: 0.5, ease: 'power2.out' })
      tl.from(sentenceTop, { opacity: 0, y: 40, duration: 0.6, ease: 'power2.out' })
      tl.from(sentenceBottom, { opacity: 0, y: 40, duration: 0.6, ease: 'power2.out', delay: 0.6 })
    })

    // Mobile : état initial invisible, déclenchement via state
    mm.add('(max-width: 576px)', () => {
      gsap.set(image, { opacity: 0, x: 70 })
      gsap.set([sentenceTop, sentenceBottom], { opacity: 0, y: 40 })
    })
  })
})

watch(
  () => props.state,
  (val) => {
    if (val === 3 && window.innerWidth <= 576 && section.value) {
      const sentenceTop = section.value.querySelector('#intro-text-sentence-top')
      const sentenceBottom = section.value.querySelector('#intro-text-sentence-bottom')
      const image = section.value.querySelector('#intro-text-img')

      const tl = gsap.timeline()
      tl.to(image, { opacity: 1, x: 0, duration: 0.5, ease: 'power2.out' })
      tl.to(sentenceTop, { opacity: 1, y: 0, duration: 0.6, ease: 'power2.out' })
      tl.to(sentenceBottom, { opacity: 1, y: 0, duration: 0.6, ease: 'power2.out', delay: 0.6 })
    }
  },
)

onBeforeUnmount(() => ctx?.revert())
</script>

<template>
  <div class="screen" id="intro-text">
    <div ref="section">
      <div class="row">
        <div
          class="col-12 col-sm-10 col-md-6 col-lg-5 offset-0 offset-sm-1 offset-md-0 offset-lg-1 offset-xl-2"
        >
          <div id="intro-text-texts-animation">
            <p id="intro-text-sentence-top">
              Le sapin porte-parole est une initiative de sensibilisation et de solidarité portée
              par l'association <em>Victime pas seule</em>, visant à soutenir les victimes de
              violences durant les <em>« Orange Days »</em>.
            </p>
            <p id="intro-text-sentence-bottom">
              Des sapins ont été installés dans plusieurs endroits en Suisse romande, notamment à la
              <em>gare de Fribourg</em>, pour recueillir des messages d'espoir et briser le silence.
            </p>
          </div>
        </div>

        <div
          class="col-12 col-sm-6 col-md-6 col-lg-5 col-xl-4 offset-0 offset-sm-6 offset-md-0 offset-lg-1 intro-text-image-col"
        >
          <div id="intro-text-img-container">
            <img
              id="intro-text-img"
              src="/img-installation.webp"
              alt="Deux personnes regardant l'installation dans la gare de Fribourg."
            />
            <img id="intro-text-visual" src="/bg-p3-v2-orange.svg" alt="" />
          </div>
        </div>
      </div>
    </div>
    <button @click="$emit('nextSection')" id="next-section">
      <span class="icon">
        <svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M4.29289 8.29289C4.68342 7.90237 5.31658 7.90237 5.70711 8.29289L12 14.5858L18.2929 8.29289C18.6834 7.90237 19.3166 7.90237 19.7071 8.29289C20.0976 8.68342 20.0976 9.31658 19.7071 9.70711L12.7071 16.7071C12.3166 17.0976 11.6834 17.0976 11.2929 16.7071L4.29289 9.70711C3.90237 9.31658 3.90237 8.68342 4.29289 8.29289Z"
            fill="currentColor"
          />
        </svg>
      </span>
    </button>
  </div>
</template>

<style scoped>
.screen {
  display: flex;
  align-items: center;
  position: relative;
}

.screen div {
  /* z-index: 1; */
}
/* Position texte */
#intro-text-texts-animation {
  margin-top: 100px;
  position: relative;
  z-index: 1;
}

em {
  line-height: 23px;
}

/* Position image */
#intro-text-img {
  max-width: 413px;
  height: auto;
}

#intro-text-img-container {
  position: relative;
}

#intro-text-visual {
  position: absolute;
  right: 0;
  top: -390px;
  width: 860px;
  height: auto;
}

.intro-text-image-col {
  padding-right: 0;
  display: flex;
  justify-content: flex-end;
}

#intro-text-sentence-top,
#intro-text-sentence-bottom {
  background-color: var(--color-light-orange);
  border-radius: 10px;
}

#next-section {
  position: absolute;
  bottom: 5%;
  left: 50%;
  transform: translateX(-50%);
  background: none;
  color: white;
  border: none;
  z-index: 10;
}

#next-section .icon {
  border: 1px solid white;
  width: 40px;
  height: 40px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  animation: pulse 3s infinite;
}

#next-section .icon svg {
  width: 24px;
}

@keyframes pulse {
  0% {
    transform: scale(1);
  }

  50% {
    transform: scale(1.3);
  }

  100% {
    transform: scale(1);
  }
}

/* Responsive */
@media (max-width: 992px) {
  #intro-text-img {
    height: auto;
    max-width: 75%;
  }
}

@media (max-width: 576px) {
  #texts-animation {
    margin-top: 0;
  }

  #intro-text-visual {
    display: none;
  }

  #next-section {
    left: 85%;
    transform: translateX(0);
  }

  /* #intro-text {
    padding-top: 50vh;
    height: 100svh !important;
    padding-bottom: 30vh;
  } */

  #intro-text .row {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
  }
}
</style>
