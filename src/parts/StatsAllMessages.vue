<script setup>
import { ref, computed, onMounted, watch, nextTick } from 'vue'
import gsap from 'gsap'
import messages from '@/data/messages-sapin-porte-paroles.json'

// Messages et filtres
// catégorie par défaut
const activeCategory = ref('category-support')

// filtrage
const filteredMessages = computed(() => {
  return messages.filter((m) => m.category === activeCategory.value)
})

// texte et espacement
const streams = ref([])

function buildMessageStream(messages) {
  const base = messages
    .map((m) => `\u00A0\u00A0\u00A0\u00A0${m.message}\u00A0\u00A0\u00A0\u00A0`)
    .join('  ')
  return base + ' ✦ ' + base
}

function updateStreams() {
  const shuffled = [...filteredMessages.value].sort(() => 0.5 - Math.random())

  streams.value = Array.from({ length: 5 }, (_, i) => {
    const rotated = shuffled.slice(i).concat(shuffled.slice(0, i))
    return buildMessageStream(rotated)
  })
}

const texts = [
  { id: '#stats-messages-text-top', duration: 28, delay: 0 },
  { id: '#stats-messages-text-middle-left', duration: 32, delay: 1 },
  { id: '#stats-messages-text-middle-right', duration: 26, delay: 1 },
  { id: '#stats-messages-text-bottom-left', duration: 34, delay: 0 },
  { id: '#stats-messages-text-bottom-right', duration: 30, delay: 1 },
]

// // animation
function startAnimations() {
  texts.forEach((t) => {
    gsap.fromTo(
      t.id,
      { attr: { startOffset: '0%' } },
      {
        attr: { startOffset: '-100%' },
        duration: t.duration,
        delay: t.delay,
        ease: 'none',
        repeat: -1,
      },
    )
  })
}

// // chargement et changement de filtre
onMounted(async () => {
  updateStreams()

  await nextTick()

  startAnimations()
})

watch(activeCategory, async () => {
  await gsap.to('textPath', {
    opacity: 0,
    duration: 0.4,
  })

  gsap.killTweensOf('textPath')

  updateStreams()

  await nextTick()

  startAnimations()

  gsap.to('textPath', {
    opacity: 1,
    duration: 0.2,
  })
})

function setFilter(category) {
  activeCategory.value = category
}
</script>

<template>
  <div class="screen">
    <div id="stats-messages-layout-content-text">
      <div id="layout-title">
        <h2>Messages du sapin porte-parole</h2>
      </div>
      <div id="filters-layout">
        <div id="filters" role="group" aria-label="Filtrer les messages par catégorie">
          <button
            :class="{ active: activeCategory === 'category-support' }"
            :aria-pressed="activeCategory === 'category-support'"
            @click="setFilter('category-support')"
          >
            Soutien émotionnel
          </button>
          <button
            :class="{ active: activeCategory === 'category-action' }"
            :aria-pressed="activeCategory === 'category-action'"
            @click="setFilter('category-action')"
          >
            Appel à l'action
          </button>
          <button
            :class="{ active: activeCategory === 'category-solidarity' }"
            :aria-pressed="activeCategory === 'category-solidarity'"
            @click="setFilter('category-solidarity')"
          >
            Solidarité collective
          </button>
          <button
            :class="{ active: activeCategory === 'category-condemnation' }"
            :aria-pressed="activeCategory === 'category-condemnation'"
            @click="setFilter('category-condemnation')"
          >
            Condamnation de la violence
          </button>
          <button
            :class="{ active: activeCategory === 'category-tributes' }"
            :aria-pressed="activeCategory === 'category-tributes'"
            @click="setFilter('category-tributes')"
          >
            Hommages aux victimes
          </button>
        </div>
      </div>
      <div></div>
    </div>
    <div id="stats-messages-tree-container">
      <svg
        class="stats-messages-tree-overlay"
        id="stats-messages-text-top"
        width="405"
        height="249"
        viewBox="0 0 405 249"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M293.956 123.479C344.456 124.227 320.456 71.979 356.956 64.479C388.114 58.0767 399.955 85.9788 396.956 108.479C394.556 126.479 377.456 168.479 350.956 168.479C294.323 168.479 300.896 210.751 257.456 200.979C194.004 186.705 164.112 229.348 129.456 192.479C105.956 167.479 101.141 177.799 52.456 163.479C14.8907 152.429 7.95607 126.479 13.956 105.479C17.8021 92.0175 43.456 82.9789 62.4561 90.4789C88.456 100.742 87.8356 114.776 109.456 126.479C163.956 155.979 172.671 127.655 202.456 136.979C251.936 152.468 254.88 122.9 293.956 123.479Z"
          fill="#F9FCFF"
        />
        <path
          id="curve-text-top"
          d="M40.02 124C163.52 204 303.02 212.5 373.02 91.5"
          stroke="none"
        />
        <g class="text-mask">
          <text>
            <textPath id="stats-messages-text-top" href="#curve-text-top" startOffset="0%">
              {{ streams[0] }}
            </textPath>
          </text>
        </g>
      </svg>

      <svg
        class="stats-messages-tree-overlay"
        id="stats-messages-text-middle-left"
        width="474"
        height="483"
        viewBox="0 0 474 483"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M352.411 282.641C381.882 303.633 415.574 289.904 434.426 296.626C453.279 303.349 463.779 326.349 455.779 345.849C450.864 357.827 423.955 384.661 381.779 354.349C339.603 324.036 316.99 369.778 275.025 342.707C227.435 312.007 217.203 348.509 187.733 315.131C144.687 266.377 108.172 275.214 89.2788 242.849C69.6088 209.153 37.2786 199.349 29.2788 167.349C21.6127 136.683 28.2788 118.849 43.7788 110.849C61.5512 101.676 78.6765 103.939 89.2788 125.849C107.326 163.142 112.435 154.141 127.779 173.349C161.6 215.685 171.61 197.838 190.279 222.849C221.293 264.399 225.379 241.714 256.701 265.085C301.041 298.168 322.939 261.648 352.411 282.641Z"
          fill="#F9FCFF"
        />
        <path
          id="curve-text-middle-left"
          d="M47.8428 143.37C115.843 264.37 202.343 316.87 432.843 338.869"
          stroke="none"
        />
        <text>
          <textPath
            id="stats-messages-text-middle-left"
            href="#curve-text-middle-left"
            startOffset="0%"
          >
            {{ streams[1] }}
          </textPath>
        </text>
      </svg>

      <svg
        class="stats-messages-tree-overlay"
        id="stats-messages-text-middle-right"
        width="493"
        height="180"
        viewBox="0 0 493 180"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M292.705 92.6172C344.289 87.3878 336.818 132.236 375.705 136.117C426.134 141.15 433.205 206.919 481.205 164.117C498.456 148.734 495.9 105.966 446.366 99.6202C391.705 92.6173 376.776 33.6172 317.705 37.1172C252.782 40.964 242.326 4.16387 205.703 12.1173C167.575 20.3975 163.987 -10.3086 116.704 8.11726C79.7383 22.5223 61.8879 3.82061 32.204 10.2123C-13.7965 20.1173 -4.36183 88.4418 39.7035 69.1173C86.4494 48.6173 97.6314 77.6913 126.203 69.1173C165.886 57.2092 162.676 73.2924 187.203 71.6173C241.265 67.925 261.655 95.7651 292.705 92.6172Z"
          fill="#F9FCFF"
        />
        <path
          id="curve-text-middle-right"
          d="M29.269 52.1381C190.769 16.6382 347.269 71.6382 454.269 156.899"
          stroke="none"
        />
        <text>
          <textPath
            id="stats-messages-text-middle-right"
            href="#curve-text-middle-right"
            startOffset="0%"
          >
            {{ streams[2] }}
          </textPath>
        </text>
      </svg>

      <svg
        class="stats-messages-tree-overlay"
        id="stats-messages-text-bottom-left"
        width="655"
        height="357"
        viewBox="0 0 655 357"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M185.384 205.53C149.225 206.866 130.908 214.702 102.172 241.944C73.4361 269.185 4.43574 278.185 4.43609 235.685C4.43641 198.185 41.6862 175.374 80.9361 174.09C120.186 172.807 132.436 130.359 211.96 123.748C268.398 119.055 301 77.0777 344.71 85.5583C408.557 97.9456 416.623 65.97 451.334 80.0984C487.472 94.8074 482.232 68.7588 531.32 81.6299C569.196 91.5614 585.868 80.7536 613.094 94.1977C646.455 110.671 653.257 124.028 647.226 139.859C641.97 153.655 623.779 162.992 602.504 151.005C551.05 122.015 555.17 150.099 530.247 137.62C493.202 119.07 480.973 149.463 458.184 140.24C401.116 117.144 394.314 158.982 359.782 149.287C309.864 135.271 312.895 173.511 273.819 174.09C218.503 174.911 221.543 204.194 185.384 205.53Z"
          fill="#F9FCFF"
        />
        <path
          id="curve-text-bottom-left"
          d="M49 235.206C160.833 172.373 408.5 75.2061 615.5 132.206"
          stroke="none"
        />
        <text>
          <textPath
            id="stats-messages-text-bottom-left"
            href="#curve-text-bottom-left"
            startOffset="0%"
          >
            {{ streams[3] }}
          </textPath>
        </text>
      </svg>

      <svg
        class="stats-messages-tree-overlay"
        id="stats-messages-text-bottom-right"
        width="581"
        height="256"
        viewBox="0 0 581 256"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M136 190.514C100.5 197.514 94 217.014 69.5008 240.514C45.0016 264.014 -0.000257015 260.514 0 220.514C8.31923e-05 207.566 18.5008 172.845 69.5008 163.014C120.501 153.182 97.0007 104.918 145.501 93.0137C200.501 79.5137 181.001 47.0051 225.501 48.5137C290.501 50.7172 308.501 9.51369 345.001 18.0137C383.001 26.863 390.501 3.01368 441.001 8.01361C479.967 11.8716 504.5 -6.48632 533.5 2.51373C600 23.1518 591 96.5136 535.5 69.0137C480 41.5137 474.441 69.0137 446.001 60.0135C406.501 47.5135 396.999 71.0553 372.5 69.0137C318.5 64.5137 326.5 98.6253 295.5 95.0137C244 89.0137 253 126.302 214.501 133.013C160 142.514 171.5 183.514 136 190.514Z"
          fill="#F9FCFF"
        />
        <path
          id="curve-text-bottom-right"
          d="M43.564 233.535C135.564 147.035 337.564 -12.4653 562.564 55.0341"
          stroke="none"
        />
        <text>
          <textPath
            id="stats-messages-text-bottom-right"
            href="#curve-text-bottom-right"
            startOffset="0%"
          >
            {{ streams[4] }}
          </textPath>
        </text>
      </svg>

      <img id="stats-messages-tree-background-desktop" src="/img-all-messages-desktop.webp" alt="" loading="lazy" />
      <img id="stats-messages-tree-background-mobile" src="/img-all-messages-mobile.webp" alt="" loading="lazy" />
    </div>
  </div>
</template>

<style scoped>
/* bouton principal */
#filters-toggle {
  font-size: 15px;
  font-weight: 700;
  border-radius: 29px;
  padding: 3px 15px 5px;
  margin-top: 10px;
  border: 1.4px solid #8fa9c8;
  background-color: var(--color-light-blue);
  color: var(--color-blue);
  cursor: pointer;
  transition:
    transform 0.4s ease,
    color 0.2s ease,
    border 0.2s ease;
}

#filters-toggle:hover {
  color: var(--color-orange);
  border-color: var(--color-orange);
  transform: scale(1.04);
}

/* Style filtres */
#filters {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 100px;
}

button {
  font-size: 15px;
  font-weight: 700;

  border-radius: 29px;
  padding: 3px 15px 5px;
  margin-top: 10px;

  border: 1.4px solid #8fa9c8;
  background-color: var(--color-light-blue);
  color: var(--color-blue);

  transition:
    transform 0.4s ease,
    color 0.2s ease,
    border 0.2s ease;
}

button:hover {
  color: var(--color-orange);
  border: 1.4px solid var(--color-orange);
  transform: scale(1.04);
}

button.active {
  color: var(--color-white);
  border: 1.4px solid var(--color-orange);
  background-color: var(--color-orange);
  transform: scale(1.04);
}

/* Mise en page titre et filtres */
#stats-messages-layout-content-text {
  padding-top: 40px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h2 {
  width: 427px;
}

/* Mise en page de toute la page */
.screen {
  display: flex;
  overflow-y: clip;
}

/* Courbes */
#stats-messages-tree-container {
  position: relative;
  height: 100%;
  pointer-events: none;
  margin-left: -100px;
}

#stats-messages-tree-background-desktop {
  /* Pour image pleine: margin-top: -100px; */
  width: 780px;
  height: auto;
}

#stats-messages-tree-background-mobile {
  display: none;
}

.stats-messages-tree-overlay {
  position: absolute;
}

/* Font */
text {
  font-family: epilogue, sans-serif;
  font-size: 22px;
  font-weight: 400;
  fill: var(--color-blue);
}

/* Position courbes */
#stats-messages-text-top {
  left: 180px;
}

#stats-messages-text-middle-left {
  top: 130px;
  left: -70px;
}

#stats-messages-text-middle-right {
  top: 260px;
  right: 0;
}

#stats-messages-text-bottom-left {
  left: -280px;
  bottom: 10px;
}

#stats-messages-text-bottom-right {
  right: -40px;
  bottom: 25px;
}

@media (max-width: 1400px) {
  #stats-messages-text-middle-left {
    top: 130px;
    left: -90px;
  }

  #stats-messages-text-middle-right {
    top: 260px;
    right: 50px;
  }

  #stats-messages-text-bottom-left {
    left: -320px;
    bottom: 10px;
  }

  #stats-messages-text-bottom-right {
    right: 50px;
    bottom: 30px;
  }
}

@media (max-width: 1200px) {
  #filters {
    width: 255px;
  }

  #stats-messages-text-top {
    left: 120px;
  }

  #stats-messages-text-middle-left {
    top: 130px;
    left: -120px;
  }

  #stats-messages-text-middle-right {
    top: 240px;
    right: 250px;
  }

  #stats-messages-text-bottom-left {
    left: -340px;
    bottom: 30px;
  }

  #stats-messages-text-bottom-right {
    right: 250px;
    bottom: 0;
  }
}

@media (max-width: 1100px) {
  #stats-messages-tree-container {
    margin-left: -150px;
  }

  #stats-messages-text-top {
    left: 90px;
  }

  #stats-messages-text-middle-left {
    top: 130px;
    left: -130px;
  }

  #stats-messages-text-middle-right {
    top: 240px;
    right: 280px;
  }

  #stats-messages-text-bottom-left {
    left: -330px;
    bottom: 30px;
  }

  #stats-messages-text-bottom-right {
    right: 290px;
    bottom: 0;
  }
}

@media (min-width: 992px) {
  .screen {
    padding-left: 60px;
  }
}

@media (max-width: 992px) {
  h2 {
    position: relative;
  }

  #filters {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 0 12px;
    width: auto;
    margin-bottom: 10px;
  }

  #stats-messages-tree-container {
    margin-left: 0;
  }

  .screen {
    flex-direction: column;
  }

  #stats-messages-text-top {
    left: 140px;
    top: -60px;
  }

  #stats-messages-text-middle-left {
    top: 100px;
    left: -40px;
  }

  #stats-messages-text-middle-right {
    top: 190px;
    right: -20px;
  }

  #stats-messages-text-bottom-left {
    left: -40px;
    bottom: 90px;
  }

  #stats-messages-text-bottom-right {
    overflow: hidden;
    display: none;
    opacity: 0;
  }
}

@media (max-width: 768px) {
  .screen {
    min-height: auto;
  }

  #filters-layout {
    position: relative;
  }

  #filters {
    position: absolute;
    z-index: 10;
  }

  #stats-messages-tree-background-desktop {
    display: none;
  }

  #stats-messages-tree-background-mobile {
    display: block;
    width: 100%;
    height: auto;
  }

  #stats-messages-text-top {
    left: 150px;
    top: 30px;
  }

  #stats-messages-text-middle-left {
    top: 50px;
    left: -100px;
  }

  #stats-messages-text-middle-right {
    top: 230px;
    right: -67px;
  }

  #stats-messages-text-bottom-left {
    left: -70px;
    bottom: -50px;
  }

  text {
    font-size: 18px;
  }
}

@media (max-width: 576px) {
  #stats-messages-text-top {
    left: 50px;
    top: 30px;
  }

  #stats-messages-text-middle-left {
    top: 80px;
    left: -100px;
  }

  #stats-messages-text-middle-right {
    top: 220px;
    right: -60px;
  }

  #stats-messages-text-bottom-left {
    overflow: hidden;
    display: none;
    opacity: 0;
  }
}
</style>
