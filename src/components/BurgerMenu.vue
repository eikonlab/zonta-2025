<script setup>
import { onMounted, nextTick } from 'vue'

onMounted(async () => {
  await nextTick()

  const sections = [
    'burger-accueil',
    'burger-recapitulatif',
    'burger-retour-image',
    'burger-informations',
  ]

  const links = document.querySelectorAll('.menu a')

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          links.forEach((link) => link.classList.remove('active'))

          const activeLink = document.querySelector(`a[href="#${entry.target.id}"]`)

          if (activeLink) activeLink.classList.add('active')
        }
      })
    },
    { threshold: 0.1 },
  )

  sections.forEach((id) => {
    const section = document.getElementById(id)
    if (section) observer.observe(section)
  })
})

onMounted(() => {})
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
    </div>
    <div></div>
  </div>
</template>

<style scoped>
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

ul {
  list-style-type: none;
  padding-left: 0;
}

li a::after {
  content: '•';
  margin-left: 8px;
  color: var(--color-orange);
  opacity: 0;
}

li a.active::after {
  opacity: 1;
}
</style>
