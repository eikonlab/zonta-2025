<script setup>
import { onMounted, nextTick } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

// Interactivité bouton burger
onMounted(() => {
  const burger = document.querySelector('.burger')
  const menu = document.querySelector('.menu')

  function toggleMenu() {
    menu.classList.toggle('is-active')
  }

  burger.addEventListener('click', toggleMenu)
})

// Animation dot
gsap.registerPlugin(ScrollTrigger)

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

    links.forEach((l) => l.classList.remove('active'))
    link.classList.add('active')

    const linkRect = link.getBoundingClientRect()
    const menuRect = link.closest('.menu').getBoundingClientRect()
    const top = linkRect.top - menuRect.top + linkRect.height / 2 - 2

    gsap.to(dot, {
      duration: 0.5,
      top: top,
      opacity: 1,
      ease: 'power2.out',
    })
  }

  moveDot(0)
})
</script>

<template>
  <div class="burger"><p>Button</p></div>
  <div class="burger-layout">
    <div class="menu">
      <ul>
        <li><a href="#burger-accueil">Accueil</a></li>
        <li><a href="#burger-recapitulatif">Récapitulatif</a></li>
        <li><a href="#burger-retour-image">Retour en image</a></li>
        <li><a href="#burger-informations">Informations</a></li>
      </ul>
      <div class="active-dot"></div>
    </div>
    <div></div>
  </div>
</template>

<style scoped>
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

a.active {
  color: var(--color-orange);
}

ul {
  list-style-type: none;
  padding-left: 15px;
}

/* Style burger menu entier */
.burger-layout {
  background-color: var(--color-orange);
  width: 230px;
  height: 100vh;
  padding: 10px 18px;

  position: fixed;
  top: 0;
  right: 0;
  z-index: 10;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.burger {
  align-self: flex-end;
}

/* Réactivité bouton */
.menu {
  position: relative;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s;
}

.menu.is-active {
  opacity: 1;
  pointer-events: auto;
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
</style>
