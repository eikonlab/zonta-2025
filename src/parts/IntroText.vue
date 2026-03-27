<script setup></script>

<template>
  <div id="intro-text">
    <div>
      <div class="row">
        <div
          class="col-12 col-sm-10 col-md-6 col-lg-5 offset-0 offset-sm-1 offset-md-0 offset-lg-1 offset-xl-2"
        >
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

        <div
          class="col-12 col-sm-6 col-md-6 col-lg-5 col-xl-4 offset-0 offset-sm-6 offset-md-0 offset-lg-1 image-col"
        >
          <div>
            <img
              src="./../../img-installation.png"
              alt="Deux personnes regardant l'installation dans la gare de Fribourg."
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  display: flex;
  align-items: center;
}

#intro-text {
  height: 200vh;
}

/* Position texte */
#texts-animation {
  margin-top: 100px;
}

/* Position image */
img {
  max-width: 413px;
  height: auto;
}

.image-col {
  padding-right: 0;
  display: flex;
  justify-content: flex-end;
}

/* Responsive */
@media (max-width: 992px) {
  img {
    height: auto;
    max-width: 100%;
  }
}

@media (max-width: 768px) {
  #texts-animation {
    margin-top: 0;
  }
}

@media (max-width: 576px) {
  .image-col {
    padding-left: 0;
  }
}
</style>
