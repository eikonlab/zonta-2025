<script setup>
import ButtonShare from './../components/ButtonShare.vue'
</script>

<template>
  <div class="screen">
    <div>
      <div class="row">
        <div class="col-10 col-lg-5 offset-1 offset-lg-1">
          <p>
            Vous êtes <strong>victime</strong> ou avez été
            <strong>victime de violences</strong> physiques, psychiques ou sexuelles ou avez besoin
            d’aide ?
            <a href="https://www.victimepasseule.ch/post/aide-aux-victimes" target="_blank">
              <strong>Voici la liste des contacts utiles.</strong>
            </a>
          </p>
          <p>
            <strong>Vous souhaitez témoigner anonymement ?</strong> Vous pouvez transmettre votre
            témoignage
            <a href="https://www.victimepasseule.ch/formulaire" target="_blank"
              ><strong>ici</strong></a
            >
            !
          </p>
        </div>
        <div class="col-10 col-lg-4 offset-1 offset-lg-1">
          <div id="outro-info-layout-responsive-emergency">
            <div id="outro-info-layout-emergency">
              <div id="outro-info-emergency">
                <p><strong>Numéros d'urgence</strong></p>
                <p>
                  Police: <strong>117</strong><br />Ambulance: <strong>144</strong><br />La main
                  tendue: <strong>143</strong><br />
                  <a href="https://www.ciao.ch/" target="_blank"><strong>Ciao.ch</strong> </a
                  ><br />Pro Juventute (pour les 11-20 ans): <strong>147</strong>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-10 col-md-7 col-lg-4 offset-1 offset-md-1 offset-lg-2">
          <p>
            Sur une idée de l'association
            <a href="https://www.victimepasseule.ch/" target="_blank">Victime pas seule</a>,
            réalisation
            <a href="https://www.zonta.ch/fr/" target="_blank">Zonta Club Fribourg</a> et
            <a href="https://www.eikon.ch/departments/eikonlab/" target="_blank">eikonlab</a>, en
            partenariat avec
            <a href="https://swiss-soroptimist.ch/fr/" target="_blank"
              >Soroptimist International Club Fribourg</a
            >
          </p>
          <ButtonShare></ButtonShare>
        </div>
      </div>
      <div class="row">
        <div class="col-12 col-sm-8 col-md-7 col-lg-5 offset-0 offset-sm-4 offset-md-5 offset-lg-7">
          <div id="outro-info-credits">
            <div id="outro-info-layout-credits-text">
              <p><strong>2026 © Victime pas seule</strong></p>
              <p>
                Réalisation
                <a href="https://www.eikon.ch/departments/eikonlab/" target="_blank"
                  ><strong>eikonlab</strong></a
                >
                <br />
                Conception du site - Oliva Baeriswyl et Flavio Rotunno<br />After movie - Laurianne
                Sauteur et Elise Mutrux
              </p>
            </div>
            <img src="/img-credits.png" alt="" />
          </div>
        </div>
      </div>
      <div class="row">
        <div
          class="col-12 col-sm-12 col-md-7 col-lg-5 offset-0 offset-sm-0 offset-md-5 offset-lg-7"
        >
          <div id="outro-info-logos">
            <a href="https://www.zonta.ch/fr/" target="_blank">
              <img src="/logo-zonta-fribourg.png" alt="Zonta Fribourg - logo" />
            </a>
            <a href="https://swiss-soroptimist.ch/fr/" target="_blank">
              <img src="/logo-soroptimist-fribourg.png" alt="Soroptimist Fribourg - logo" />
            </a>
            <a href="https://www.eikon.ch/" target="_blank">
              <img id="outro-info-eikon" src="/logo-eikon.png" alt="eikon - logo" />
            </a>
            <a href="https://www.fr.ch/" target="_blank">
              <img src="/logo-etat-fribourg-staat-freiburg.png" alt="Etat de Fribourg - logo" />
            </a>
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
  align-items: flex-end;
}

/* Liens */
a {
  color: var(--color-blue);
  transition: all 0.2s ease;
  text-decoration: underline 1.4px;
}

a:hover {
  opacity: 0.6;
}

/* Mise en page encadré numéros */
#outro-info-emergency,
#outro-info-emergency a {
  color: var(--color-orange);
}

#outro-info-emergency {
  border: solid 1.4px var(--color-orange);
  border-radius: 29px;
  padding: 30px;
}

#outro-info-layout-emergency {
  max-width: 320px;
}

/* Crédits */
#outro-info-credits p,
#outro-info-credits strong {
  font-size: 15px;
  line-height: 16px;
  position: relative;
  z-index: 2;
}

#outro-info-credits strong {
  font-weight: 600;
}

#outro-info-credits {
  position: relative;
  margin-top: -30px;
  padding-bottom: 20px;
}

#outro-info-credits img {
  opacity: 50%;
  width: 122px;

  position: absolute;
  top: -50px;
  left: -4px;
  z-index: 1;
}

#outro-info-layout-credits-text {
  margin-left: 30px;
}

#outro-info-logos {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 5px 0 20px;
}

#outro-info-logos img {
  width: 80px;
  height: 100%;
}

#outro-info-logos #outro-info-eikon {
  width: 95px;
  height: 100%;
}

/* Bouton */

/* Responsive */
@media (min-width: 576px) and (max-width: 992px) {
  #outro-info-layout-responsive-emergency {
    display: flex;
    justify-content: flex-end;
  }
}

@media (max-width: 992px) {
  .screen {
    height: auto !important;
  }

  #outro-info-layout-emergency {
    margin: 50px 0 180px;
  }

  #outro-info-credits {
    margin-top: 100px;
  }
}

@media (max-width: 576px) {
  #outro-info-layout-emergency {
    max-width: 100%;
  }
}
</style>
