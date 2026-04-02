<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const section = ref(null)
let ctx

onMounted(() => {
  ctx = gsap.context(() => {
    const sentenceTop = section.value.querySelector('#intro-text-sentence-top')
    const sentenceBottom = section.value.querySelector('#intro-text-sentence-bottom')
    const image = section.value.querySelector('#intro-text-img')

    const tl = gsap.timeline({
      scrollTrigger: {
        trigger: section.value,
        start: 'center 80%',
        end: () => `+=${window.innerHeight * 0.6}`,
        toggleActions: 'play reverse play reverse',
      },
    })
    tl.from(image, {
      opacity: 0,
      x: 70,
      duration: 0.5,
      ease: 'power2.out',
    })

    tl.from(sentenceTop, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
    })

    tl.from(sentenceBottom, {
      opacity: 0,
      y: 40,
      duration: 0.6,
      ease: 'power2.out',
      delay: 0.6,
    })
  })
})

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
              violences durant les <em>« Orange Day »</em>.
            </p>
            <p id="intro-text-sentence-bottom">
              Des sapins ont étés installés dans plusieurs endroits en Suisse romande, notamment à
              la
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
              src="/img-installation.png"
              alt="Deux personnes regardant l'installation dans la gare de Fribourg."
            />
            <img id="intro-text-visual" src="/bg-p3-v2-orange.svg" alt="" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  display: flex;
  align-items: center;
}

.screen div {
  z-index: 1;
}
/* Position texte */
#intro-text-texts-animation {
  margin-top: 100px;
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

/* Responsive */
@media (max-width: 992px) {
  #intro-text-img {
    height: auto;
    max-width: 100%;
  }
}

@media (max-width: 576px) {
  #texts-animation {
    margin-top: 0;
  }

  #intro-text {
    padding-top: 50vh;
    height: 200vh !important;
    padding-bottom: 30vh;
  }

  #intro-text .row {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
  }
}
</style>
