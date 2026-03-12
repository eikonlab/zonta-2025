<script setup>
import ButtonScroll from './../components/ButtonScroll.vue'
</script>

<template>
  <div class="screen">
    <div class="container">
      <div class="row">
        <div class="col-12 col-sm-10 col-md-8 col-lg-6 offset-0 offset-xl-1">
          <div id="texts-animation">
            <p>
              Le sapin porte-parole est une initiative de sensibilisation et de solidarité portée
              par l'association <em>Victime pas seule</em>, visant à soutenir les victimes de
              violences durant les <em>« Orange Day »</em>.
            </p>
            <p>
              Des sapins ont étés installés dans plusieurs endroits en Suisse romande, notamment à
              la
              <em>gare de Fribourg</em>, pour recueillir des messages d'espoir et briser le silence.
            </p>
          </div>
        </div>

        <div class="col-12 col-md-6 col-lg-5 col-xl-4 offset-lg-1">
          <div class="image-wrapper">
            <img
              src="./../../img-installation.png"
              alt="Deux personnes regardant l'installation dans la gare de Fribourg."
            />
          </div>
        </div>
      </div>

      <ButtonScroll></ButtonScroll>
    </div>
  </div>
</template>

<style scoped>
.screen {
  height: 100vh;
  position: relative;
}

/* Position image */
.image-wrapper {
  position: absolute; /* sort du padding de la colonne */
  top: 0;
  right: 0; /* collé au bord du viewport */
  height: 100%;
}

/* L'image elle-même */
.image-wrapper img {
  height: 100%; /* adapte à la hauteur de la ligne */
  max-width: none; /* ignore le max-width de la colonne */
}

/* .image-wrapper {
  position: relative;
  width: 100%;
  height: auto;
}

.image-wrapper img {
  position: absolute;
  right: 0;
  top: 0;
  max-width: 100%;
  height: auto;
} */
</style>
