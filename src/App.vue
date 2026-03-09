<script setup>
import PartOutro from './parts/PartOutro.vue'
import PartIntro from './parts/PartIntro.vue'
import PartStats from './parts/PartStats.vue'
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

<style scoped></style>
