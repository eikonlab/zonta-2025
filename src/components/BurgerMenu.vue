<script setup>
import { onMounted, nextTick } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

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
    const linkRect = link.getBoundingClientRect()
    const menuRect = link.closest('.menu').getBoundingClientRect()
    const top = linkRect.top - menuRect.top + linkRect.height / 2 - 4 // centre du dot

    gsap.to(dot, {
      duration: 0.5,
      top: top,
      opacity: 1,
      ease: 'power2.out',
    })
  }

  // initial position
  moveDot(0)
})
</script>

<template>
  <div class="burger-menu">
    <div class="burger"><p>Button</p></div>
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
  line-height: 30px;
  color: var(--color-blue);
  text-decoration: none;
  transition: color 0.2s ease;
}

a:hover {
  color: var(--color-orange);
}

ul {
  list-style-type: none;
  padding-left: 0;
}

/* Style burger menu entier */
.burger-menu {
  background-color: var(--color-white);
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

/* Style lien */
li a::after {
  content: '•';
  margin-left: 8px;
  color: var(--color-orange);
  opacity: 0;
}

li a.active::after {
  opacity: 1;
}

/* Point activé */
.menu {
  position: relative;
}

.menu li {
  position: relative;
}

.active-dot {
  background-color: var(--color-orange);
  width: 8px;
  height: 8px;
  border-radius: 50%;

  position: absolute;
  top: 0;
  left: 100%;
  transform: translateY(0);
}
</style>
