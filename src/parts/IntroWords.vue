<script setup></script>

<template>
  <div class="screen" id="intro-words">
    <div id="layout-all-words">
      <div class="row">
        <div class="col-10 col-lg-12 offset-2 offset-lg-0">
          <div id="layout-courage">
            <p id="word-courage">Courage</p>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-11 offset-1">
          <p id="word-espoir">Espoir</p>
        </div>
      </div>
      <div class="row">
        <div class="col-7 offset-5">
          <p id="word-soutien">Soutien</p>
        </div>
      </div>
      <div class="row">
        <div class="col-5 offset-6 offset-sm-7">
          <p id="word-respect">Respect</p>
        </div>
      </div>
      <div class="row">
        <div class="col-10 offset-2">
          <p id="word-solidarite">Solidarité</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.screen {
  height: 100vh;

  display: flex;
  align-items: center;
}

/* Texte */
p {
  font-family: arima, sans-serif;
  font-size: 68px;
  font-weight: 600;

  background-color: var(--color-light-orange);
  display: inline-block;
  padding: 30px;
  border-radius: 100px;
}

/* Mise en page centrée des mots */
#layout-all-words {
  width: 100%;
}

/* Mise en page mot Courage */
#layout-courage {
  display: flex;
  justify-content: flex-end;
}

/* Placement précis des mots */
#word-espoir {
  margin-top: -50px;
}

#word-soutien {
  margin-top: 20px;
}

#word-respect {
  margin-top: 60px;
}

#word-solidarite {
  margin-top: 30px;
}

/* Responsive */
@media (max-width: 992px) {
  .screen {
    height: auto;
  }

  #layout-courage {
    display: flex;
    justify-content: flex-start;
  }

  #word-espoir {
    margin-top: 60px;
  }

  #word-soutien {
    margin-top: 70px;
  }

  #word-respect {
    margin-top: 90px;
  }

  #word-solidarite {
    margin-top: 20px;
  }
}

@media (max-width: 768px) {
  p {
    font-size: 36px;
    padding: 20px;
  }
}
</style>
