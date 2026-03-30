<script setup></script>

<template>
  <div class="screen">
    <div>
      <div class="row">
        <div class="col-12">
          <div id="layout-page">
            <div id="layout-number">
              <p id="big-text">185</p>
              <p id="sentence-number-messages">Messages <em>récoltés</em></p>
            </div>
            <div id="layout-support-sentance">
              <p>
                Tant de messages
                <em
                  >d'amour <img src="./../../img-icon-words-heart.png" id="icon-heart" alt=""
                /></em>
                et de
                <em>soutien <img src="./../../img-icon-words-hand.png" id="icon-hand" alt="" /></em>
                partagés cette année
              </p>
            </div>
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

/* Font */
#big-text {
  font-family: arima, sans-serif;
  font-size: 250px;
  font-weight: 400;
  line-height: 250px;
  margin: 0;
  height: 250px;
}

/* Mise en page */
#layout-page {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  padding-top: 10%;
}

#layout-number {
  display: flex;
  align-items: baseline;
}

/* Icones */
em {
  position: relative;
}

img {
  width: 38px;
  height: auto;
  position: absolute;
  opacity: 0.3;
}

#icon-heart {
  top: -38px;
  right: -20px;
}

#icon-hand {
  bottom: -38px;
  right: -20px;
}

@media (max-width: 1253px) {
  #icon-hand {
    right: -40px;
  }
}

@media (max-width: 1216px) {
  #icon-heart {
    top: -64px;
    right: -20px;
  }

  #icon-hand {
    bottom: -68px;
    right: -40px;
  }
}

@media (max-width: 1200px) {
  #layout-page {
    flex-direction: column;
  }

  #layout-support-sentance {
    margin-top: 50px;
    text-align: right;
  }

  #icon-heart {
    top: -38px;
    right: -20px;
  }

  #icon-hand {
    bottom: -38px;
    right: -20px;
  }
}

@media (min-width: 992px) {
  .screen {
    padding-left: 70px;
  }

  #sentence-number-messages {
    width: 210px;
  }
}

@media (max-width: 576px) {
  #big-text {
    font-family: arima, sans-serif;
    font-size: 140px;
    font-weight: 400;
    line-height: 250px;
    margin: 0;
    height: 250px;
  }

  #icon-hand {
    bottom: -38px;
    right: -20px;
  }
}

@media (max-width: 531px) {
  #big-text {
    font-family: arima, sans-serif;
    font-size: 140px;
    font-weight: 400;
    line-height: 250px;
    margin: 0;
    height: 250px;
  }

  #icon-hand {
    bottom: -64px;
    right: -20px;
  }

  #layout-support-sentance {
    padding-left: 40px;
  }
}

@media (max-width: 500px) {
  #icon-hand {
    bottom: -64px;
    right: 0;
  }
}

@media (max-width: 422px) {
  #icon-hand {
    bottom: -68px;
    right: 5px;
  }
}
</style>
