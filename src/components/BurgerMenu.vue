<script setup>
import { onMounted, nextTick } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

// // Couleur bouton burger

onMounted(async () => {
  await nextTick()

  const circle = document.querySelector('.circle')
  const dot = document.querySelector('.active-dot')
  const links = document.querySelectorAll('.menu a')

  // Sections pour l'icône
  const sectionsAlt = ['burger-accueil', 'burger-retour-image']
  const sectionsAll = [
    'burger-accueil',
    'burger-recapitulatif',
    'burger-retour-image',
    'burger-informations',
  ]

  // IntersectionObserver pour couleur icône au scroll
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) return
        const id = entry.target.id

        circle.classList.remove('alt-burger', 'active-icon')

        if (id === 'burger-recapitulatif') circle.classList.add('active-icon')
        else if (sectionsAlt.includes(id)) circle.classList.add('alt-burger')
      })
    },
    { threshold: [0.25, 0.75] },
  )

  sectionsAll.forEach((id) => {
    const section = document.getElementById(id)
    if (section) observer.observe(section)
  })

  // Point actif et couleur au clic
  links.forEach((link, index) => {
    link.addEventListener('click', (e) => {
      e.preventDefault()
      const targetId = link.getAttribute('href').replace('#', '')
      const section = document.getElementById(targetId)
      if (!section) return

      // Scroll smooth
      section.scrollIntoView({ behavior: 'smooth' })

      // Icône couleur immédiate
      circle.classList.remove('alt-burger', 'active-icon')
      if (targetId === 'burger-recapitulatif') circle.classList.add('active-icon')
      else if (sectionsAlt.includes(targetId)) circle.classList.add('alt-burger')
    })
  })

  // Dot qui suit les sections au scroll
  sectionsAll.forEach((id, index) => {
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
    const top = linkRect.top - menuRect.top + linkRect.height / 2 - 4.5 // centre le dot 9px

    gsap.to(dot, {
      duration: 0.5,
      top: top,
      opacity: 1,
      ease: 'power2.out',
    })
  }

  moveDot(0) // dot au premier lien
})

// TEST QUI FONCTIONNE MAL (CHANGEMENT DE LA COULEUR BURGER)
// onMounted(async () => {
//   await nextTick()

//   const circle = document.querySelector('.circle')

//   // Sections avec fond orange
//   const sectionsAlt = ['burger-accueil', 'burger-retour-image']

//   // Toutes les sections
//   const sectionsAll = [
//     'burger-accueil',
//     'burger-recapitulatif',
//     'burger-retour-image',
//     'burger-informations',
//   ]

//   const observer = new IntersectionObserver(
//     (entries) => {
//       entries.forEach((entry) => {
//         const id = entry.target.id

//         // Retirer les classes avant d'ajouter la bonne
//         circle.classList.remove('alt-burger', 'active-icon')

//         if (id === 'burger-recapitulatif') {
//           // priorité active
//           circle.classList.add('active-icon')
//         } else if (sectionsAlt.includes(id)) {
//           circle.classList.add('alt-burger')
//         }
//       })
//     },
//     { threshold: [0.25, 0.75] }, // déclenche entre 25% et 75% visible
//   )

//   sectionsAll.forEach((id) => {
//     const section = document.getElementById(id)
//     if (section) observer.observe(section)
//   })
// })

// Interactivité bouton burger
onMounted(() => {
  const burger = document.querySelector('.burger')
  const menu = document.querySelector('.menu')

  function toggleMenu() {
    menu.classList.toggle('is-active')
  }

  burger.addEventListener('click', toggleMenu)
})

// TEST QUI FONCTIONNE (ANIMATION DU POINT)
// onMounted(async () => {

//   await nextTick()

//   const sections = [
//     'burger-accueil',
//     'burger-recapitulatif',
//     'burger-retour-image',
//     'burger-informations',
//   ]

//   const links = document.querySelectorAll('.menu a')
//   const dot = document.querySelector('.active-dot')

//   sections.forEach((id, index) => {
//     const section = document.getElementById(id)
//     if (!section) return

//     ScrollTrigger.create({
//       trigger: section,
//       start: 'top center',
//       end: 'bottom center',
//       onEnter: () => moveDot(index),
//       onEnterBack: () => moveDot(index),
//     })
//   })

//   function moveDot(index) {
//     const link = links[index]

//     links.forEach((l) => l.classList.remove('active'))
//     link.classList.add('active')

//     const linkRect = link.getBoundingClientRect()
//     const menuRect = link.closest('.menu').getBoundingClientRect()
//     const top = linkRect.top - menuRect.top + linkRect.height / 2 - 2

//     gsap.to(dot, {
//       duration: 0.5,
//       top: top,
//       opacity: 1,
//       ease: 'power2.out',
//     })
//   }

//   moveDot(0)
// })
</script>

<template>
  <div class="burger-menu">
    <div class="burger">
      <div class="circle">
        <div class="bar-icon">
          <div class="bar bar-top"></div>
          <div class="bar bar-middle"></div>
          <div class="bar bar-bottom"></div>
        </div>
      </div>
    </div>
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

  transition:
    background-color 0.3s,
    border-color 0.3s;
}

.bar-icon {
  height: 18px;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: end;
}

.bar {
  height: 4px;
  border-radius: 20px;
}

.bar-top {
  width: 18px;
  background-color: var(--color-blue);
  opacity: 0.6;
}

.bar-middle {
  width: 21px;
  background-color: var(--color-blue);
}

.bar-bottom {
  width: 13px;
  background-color: var(--color-blue);
  opacity: 0.6;
}

/* Style icone burger alternatif */
.circle.alt-burger {
  background-color: var(--color-light-orange);
  border: 1.4px solid var(--color-white);
}

.circle.alt-burger .bar-top,
.circle.alt-burger .bar-middle,
.circle.alt-burger .bar-bottom {
  background-color: var(--color-white);
}

.circle.active-icon {
  background-color: var(--color-white);
  border: 1.4px solid var(--color-blue);
}

.circle.active-icon .bar-top,
.circle.active-icon .bar-middle,
.circle.active-icon .bar-bottom {
  background-color: var(--color-blue);
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
  z-index: 10;
}

/* Bouton du burger menu */
.burger {
  position: absolute;
  z-index: 20;
  top: 10px;
  right: 16px;
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
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}

.menu.is-active {
  opacity: 1;
  pointer-events: auto;
}

.burger-layout:has(.menu.is-active) {
  background-color: var(--color-white);
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
