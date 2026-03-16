<script setup></script>

<template>
  <div class="screen">
    <div class="row">
      <div class="col-10">
        <div id="layout-number">
          <p id="big-text">185</p>
          <p id="sentence-number-messages">Messages <em>récoltés</em></p>
          <div id="sentence-love-messages">
            <img src="./../../img-icon-words-heart.png" id="icon-heart" alt="" />
            <p>Tant de messages <em>d'amour</em> et de <em>soutien</em> partagés cette année</p>
            <img src="./../../img-icon-words-hand.png" id="icon-hand" alt="" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
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
#layout-number {
  padding-top: 30%;
  display: flex;
  justify-content: space-around;
  align-items: baseline;
}

#sentence-number-messages {
  width: 300px;
}

#sentence-love-messages {
  align-self: flex-start;
  position: relative;
}

/* Icones */
img {
  width: 38px;
  height: auto;
  position: absolute;
  opacity: 0.3;
}

#icon-heart {
  top: -40px;
  right: 170px;
}

#icon-hand {
  bottom: 2px;
  right: 20px;
}
</style>
