<script setup>
import { onMounted, nextTick, inject, watch, ref } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const isIntroDone = inject('isIntroDone')
const isMenuOpen = ref(false)

watch(isIntroDone, (newVal) => {
  if (newVal) {
    const circle = document.querySelector('.circle')
    circle.classList.remove('alt-burger')
  }
})

// Interactivité bouton burger
onMounted(() => {
  const burger = document.querySelector('.burger')
  const menu = document.querySelector('.menu')

  function toggleMenu() {
    menu.classList.toggle('is-active')
    isMenuOpen.value = !isMenuOpen.value
  }

  burger.addEventListener('click', toggleMenu)
})

// Animation du point en fonction de la section
onMounted(async () => {
  await nextTick()

  const sections = [
    'burger-accueil',
    'burger-recapitulatif',
    'burger-retour-image',
    'burger-informations',
  ]

  const links = document.querySelectorAll('.menu a')
  const dot = document.querySelector('.active-dot')

  sections.forEach((id, index) => {
    const section = document.getElementById(id)
    if (!section) return

    ScrollTrigger.create({
      trigger: section,
      start: 'top center',
      end: 'bottom center',
      onEnter: () => moveDot(index),
      onEnterBack: () => moveDot(index),
    })
  })

  function moveDot(index) {
    const link = links[index]

    // Read layout BEFORE DOM changes to avoid forced reflow
    const linkRect = link.getBoundingClientRect()
    const menuRect = link.closest('.menu').getBoundingClientRect()
    const top = linkRect.top - menuRect.top + linkRect.height / 2 - 2

    links.forEach((l) => l.classList.remove('active'))
    link.classList.add('active')

    gsap.to(dot, {
      duration: 0.5,
      top: top,
      opacity: 1,
      ease: 'power2.out',
    })
  }

  moveDot(0)
})

// Changement couleur bouton en fonction de section et clic

onMounted(async () => {
  await nextTick()

  const circle = document.querySelector('.circle')
  const burger = document.querySelector('.burger')

  const sections = document.querySelectorAll('.burger-orange, .burger-blue')

  sections.forEach((section) => {
    ScrollTrigger.create({
      trigger: section,
      start: 'top top',
      end: 'bottom top',

      // markers: true,

      onEnter: () => updateBurger(section),
      onEnterBack: () => updateBurger(section),
    })
  })

  function updateBurger(section) {
    circle.classList.remove('alt-burger')

    if (section.classList.contains('burger-orange')) {
      circle.classList.add('alt-burger')
    }
  }

  // ouverture menu
  burger.addEventListener('click', () => {
    circle.classList.toggle('active-icon')
  })
})
</script>

<template>
  <div class="burger-menu">
    <button
      class="burger"
      type="button"
      :aria-expanded="isMenuOpen.toString()"
      aria-label="Menu de navigation"
      aria-controls="burger-nav-menu"
    >
      <div class="circle alt-burger">
        <div class="bar-icon" aria-hidden="true">
          <div class="bar bar-top"></div>
          <div class="bar bar-middle"></div>
          <div class="bar bar-bottom"></div>
        </div>
      </div>
    </button>
    <div class="burger-layout">
      <nav class="menu" id="burger-nav-menu" aria-label="Navigation principale">
        <ul>
          <li><a href="#burger-accueil">Accueil</a></li>
          <li><a href="#burger-recapitulatif">Récapitulatif</a></li>
          <li><a href="#burger-retour-image">Retour en image</a></li>
          <li><a href="#burger-informations">Informations</a></li>
        </ul>
        <div class="active-dot" aria-hidden="true"></div>
      </nav>
    </div>
  </div>
</template>

<style scoped>
/* Style icone burger */
.circle {
  width: 50px;
  height: 50px;
  background-color: var(--color-light-blue);

  border: 1.4px solid #8fa9c8;
  border-radius: 50%;

  display: flex;
  justify-content: center;
  align-items: center;

  transition: all 0.3s ease;
}

.bar-icon {
  height: 15px;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: end;
}

.bar {
  background-color: var(--color-blue);
  height: 3px;
  border-radius: 20px;

  transition: all 0.3s ease;
}

.bar-top {
  width: 18px;
  opacity: 0.6;
}

.bar-middle {
  width: 21px;
}

.bar-bottom {
  width: 13px;

  opacity: 0.6;
}
/* Style lien */
a {
  font-family: epilogue, sans-serif;
  font-size: 20px;
  font-weight: 400;
  color: var(--color-blue);
  text-decoration: none;
  transition: all 0.2s ease;
  opacity: 1;
}

a:hover {
  opacity: 0.6;
}

li {
  transition: all 0.4s ease;
}

li:hover {
  transform: scale(1.03);
}

a.active {
  color: var(--color-orange);
}

ul {
  list-style-type: none;
  padding-left: 15px;
}

/* Position burger menu entier */
.burger-menu {
  position: fixed;
  top: 0;
  right: 0;
  z-index: 20;
  pointer-events: none;
}

/* Bouton de l'icone du burger */
.burger {
  appearance: none;
  background: none;
  border: none;
  padding: 0;

  position: absolute;
  z-index: 20;
  top: 10px;
  right: 16px;

  transition: transform 0.2s ease;
  pointer-events: all;
}

.burger:hover {
  cursor: pointer;
}

.burger:hover .circle {
  transform: scale(1.16);
}

/* Style et position burger menu activé */
.burger-layout {
  background-color: none;
  width: 230px;
  height: 100vh;
  padding: 10px 18px;

  display: flex;
  flex-direction: column;
  justify-content: center;

  pointer-events: none;
  transition: background-color 0.3s ease;
}

/* Menu ouvert */
.menu {
  position: relative;
}

.burger-layout {
  transform: translateX(100%);
  opacity: 0;
  transition: all 0.3s ease;
  will-change: transform;
}

.burger-layout:has(.menu.is-active) {
  background-color: var(--color-white);
  pointer-events: auto;
  transform: translateX(0);
  opacity: 1;
}

/* Point activé */
.active-dot {
  background-color: var(--color-orange);
  width: 9px;
  height: 9px;
  border-radius: 50%;

  position: absolute;
  top: 0;
  left: 0;
  transform: translateY(0);
}

/* Changement de couleur section et clic */
.circle.alt-burger {
  background-color: var(--color-light-orange);
  border: 1.4px solid #ffffff;
}

.circle.alt-burger .bar {
  background-color: #ffffff;
}

.circle.active-icon {
  background-color: var(--color-white);
  border: 1.4px solid #8fa9c8;
  transform: scale(1.16);
}

.circle.active-icon .bar {
  background-color: var(--color-blue);
}

.circle:hover {
  background-color: var(--color-light-blue);
  border: 1.4px solid #ff9c56;
}

.circle:hover .bar {
  background-color: var(--color-orange);
}
</style>
