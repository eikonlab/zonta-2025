<script setup></script>

<template>
  <div class="screen">
    <div>
      <div class="row">
        <div class="col-12 col-lg-4 order-2 order-lg-1" id="outro-media-layout-img">
          <img
            src="/img-side-installation.webp"
            alt="25 novembre, journée internationale de lutte pour l'élimination de la violence à l'égard des femmes, suivi de la quinzaine d'activisme sur le même sujet."
            id="outro-media-img"
            loading="lazy"
          />
          <img
            src="/bg-outro-p2-light-blue.svg"
            alt=""
            id="outro-media-img-visual"
            loading="lazy"
          />
        </div>
        <div class="col-10 col-lg-7 col-xl-6 offset-1 offset-lg-0 order-1 order-lg-2">
          <h2>La presse et la radio en parlent</h2>
          <div class="row">
            <div class="col-10 offset-2">
              <a
                href="https://www.laliberte.ch/articles/regions/canton/la-gare-de-fribourg-accueille-un-sapin-porte-paroles-1250121"
                target="_blank"
              >
                <p>
                  <strong>La Liberté</strong> - Pour lutter contre les violences faites aux femmes.
                  La gare de Fribourg accueille un sapin porte-paroles
                </p>
              </a>
            </div>
            <div class="col-12 col-sm-8 offset-sm-4">
              <a
                href="https://frapp.ch/fr/articles/stories/sapin-porte-parole-violences-contre-les-femmes-fribourg"
                target="_blank"
              >
                <p>
                  <strong>Frapp</strong> - Violences faites aux femmes: un sapin pour briser le
                  silence
                </p>
              </a>
            </div>
            <div class="col-10 offset-2">
              <a
                href="https://www.rts.ch/play/tv/12h45/video/12h45?urn=urn:rts:video:a526174d-c029-30df-bcf9-d24f3859f5ef"
                target="_blank"
              >
                <p>
                  <strong>RTS</strong> – Journée internationale pour l’élimination de la violence à
                  l’égard des femmes
                </p>
              </a>
            </div>
            <div class="col-12">
              <a
                href="https://latele.ch/emissions/info-fribourg/info-fribourg-s-2025-e-192"
                target="_blank"
              >
                <p><strong>La Télé</strong> - Journal du 25 novembre 2025</p>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen div {
  z-index: 1;
}

.screen {
  display: flex;
  align-items: center;
}

/* Font */
h2 {
  margin: 0 0 30px;
}

a {
  color: var(--color-blue);
  transition: all 0.2s ease;
  text-decoration: underline 1.4px;
}

p {
  transition: all 0.4s ease;
  margin-bottom: 30px;
  background-color: var(--color-light-blue);
  border-radius: 10px;
  display: inline-block;
}

a:hover p {
  transform: scale(1.02);
  opacity: 0.6;
}

img {
  width: 100%;
  height: auto;
  max-width: 392px;
}

/* Image */
#outro-media-layout-img {
  padding-left: 0;
  position: relative;
}

#outro-media-img-visual {
  position: absolute;
  left: 0;
  top: -400px;
  width: auto;
  height: 1000px;
}

@media (max-width: 992px) {
  #outro-media-layout-img {
    padding: 12px 0;
    z-index: -1;
  }

  img {
    margin-top: 50px;
  }

  h2 {
    margin: 40px 0 30px;
  }
}

@media (max-width: 992px) {
  .screen {
    height: auto;
  }

  img {
    margin: 50px 0 200px;
  }
}

@media (max-width: 576px) {
  img {
    max-width: 100%;
  }

  img {
    margin: 200px 0;
  }
}
</style>
