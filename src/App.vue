<script setup>
import PartOutro from './sections/SectionOutro.vue'
import PartIntro from './sections/SectionIntro.vue'
import PartStats from './sections/SectionStats.vue'
import BurgerMenu from './components/BurgerMenu.vue'

import { onMounted, ref } from 'vue'
import { gsap } from 'gsap'
</script>

<template>
  <header>
    <PartIntro></PartIntro>
  </header>
  <main>
    <PartStats></PartStats>
  </main>
  <footer>
    <PartOutro></PartOutro>
  </footer>
</template>

<style scoped>
header {
  padding-top: 100px;
  background-color: var(--color-light-orange);
  color: var(--color-white);
}
</style>
