<script setup></script>

<template>
  <div class="screen">
    <div>
      <h3>Messages les plus récurrents</h3>
      <div class="row">
        <div class="col-12">
          <div id="layout-sentence-top">
            <div>
              <p class="small-text">Tu n'es</p>
              <p class="big-text">pas seule</p>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-md-7 col-lg-6 offset-md-2 offset-lg-3 offset-xl-4">
          <div id="layout-sentences">
            <div id="sentence-violence">
              <p class="small-text">La</p>
              <p class="big-text">violence</p>
              <p class="small-text specific-position-violence" id="specific-margin-violence-bottom">
                n'est
              </p>
              <p class="big-text specific-position-violence">jamais acceptable</p>
            </div>
            <div id="sentence-believe">
              <p class="small-text">Je te</p>
              <p class="big-text">crois</p>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <div id="sentence-report">
            <p class="small-text" id="specific-position-dont">N'aie</p>
            <p class="big-text" id="specific-position-scared">pas peur</p>
            <p class="small-text" id="specific-margin-report-top-bottom">de</p>
            <p class="big-text">dénoncer</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  padding-top: 6%;
}

/* Fonts */
.small-text {
  font-family: arima, sans-serif;
  font-size: 20px;
  font-weight: 300;
  line-height: 20px;
  margin: 0;
}

.big-text {
  font-family: arima, sans-serif;
  font-size: 38px;
  font-style: normal;
  font-weight: 600;
  line-height: 30px;
  margin: 0;
}

/* Mise en page */
#layout-sentence-top {
  display: flex;
  justify-content: center;
  margin-bottom: 120px;
}

#layout-sentences {
  display: flex;
  justify-content: space-between;
}

/* Postion horizontal des mots */
#specific-margin-report-top-bottom {
  margin-top: 7px;
  padding-left: 90px;
}

#specific-margin-violence-bottom {
  margin: 6px 0;
}

#layout-sentence-top .small-text {
  padding-left: 20px;
}

#specific-position-scared {
  padding-left: 80px;
}

#specific-position-dont {
  padding-left: 60px;
}

.specific-position-violence {
  padding-left: 80px;
}

#sentence-believe .big-text {
  padding-left: 20px;
}

/* Responsive */
@media (min-width: 992px) {
  .screen {
    padding-left: 60px;
  }
}

@media (max-width: 992px) {
  #sentence-violence {
    margin-bottom: 100px;
  }
}

@media (max-width: 830px) {
  #layout-sentences {
    flex-direction: column-reverse;
  }

  #sentence-violence {
    margin-bottom: 60px;
  }

  #layout-sentence-top {
    margin-bottom: 40px;
  }

  #sentence-believe {
    align-self: flex-end;
  }

  #sentence-report {
    margin-left: 30px;
  }
}

@media (max-width: 768px) {
  .small-text {
    font-size: 16px;
    line-height: 16px;
  }

  .big-text {
    font-size: 30px;

    line-height: 24px;
  }
}

@media (max-width: 576px) {
  #layout-sentence-top {
    margin-right: 40px;
    justify-content: flex-end;
  }
}
</style>
