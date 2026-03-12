<script setup>
import ButtonScroll from './../components/ButtonScroll.vue'
</script>

<template>
  <div class="screen">
    <div class="row">
      <p>
        Le sapin porte-parole est une initiative de sensibilisation et de solidarité portée par
        l'association <em>Victime pas seule</em>, visant à soutenir les victimes de violences durant
        les <em>« Orange Day »</em>.
      </p>
      <p>
        Des sapins ont étés installés dans plusieurs endroits en Suisse romande, notamment à la
        <em>gare de Fribourg</em>, pour recueillir des messages d'espoir et briser le silence.
      </p>

      <img
        src="./../../img-installation.png"
        alt="Deux personnes regardant l'installation dans la gare de Fribourg."
      />

      <ButtonScroll></ButtonScroll>
    </div>
  </div>
</template>

<style scoped>
.screen {
  height: 100vh;
}
</style>
