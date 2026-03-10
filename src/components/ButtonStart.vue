<script setup></script>

<template>
  <div>
    <a href="" class="button-wrapper">
      <div class="button-extern"></div>
      <div class="button-intern">
        <p>
          <strong>Débuter <br />l'expérience</strong>
        </p>
      </div>
    </a>
  </div>
</template>

<style scoped>
.button-wrapper {
  display: inline-block;
  position: relative;
  width: 172px;
  height: 172px;
}

.button-intern p {
  text-align: center;
  color: var(--color-white);
}

.button-extern,
.button-intern {
  border-radius: 50%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 0.5s ease;
}

/* Grand cercle de base */
.button-extern {
  border: 1.4px solid var(--color-white);
  width: 172px;
  height: 172px;
  z-index: 1;
}

/* Petit cercle de base */
.button-intern {
  background-color: #ffb27b;
  width: 106px;
  height: 106px;
  z-index: 2;
}

/* Hover */

.button-wrapper:hover .button-extern {
  width: 150px;
  height: 150px;
  z-index: 2;
}

.button-wrapper:hover .button-intern {
  width: 172px;
  height: 172px;
  z-index: 1;
}

/* .button-wrapper {
  display: inline-block;
  position: relative;
  width: 172px;
  height: 172px;
}

.button-extern,
.button-intern {
  border-radius: 100px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: 0.5s;
  display: flex;
  justify-content: center;
  align-items: center;
}

.button-extern {
  width: 172px;
  height: 172px;
  border: 1.4px solid var(--color-white);
  background-color: transparent;
  z-index: 1;
}

.button-intern {
  width: 106px;
  height: 106px;
  background-color: #ffb27b;
  z-index: 2;
}

.button-intern p {
  text-align: center;
  color: var(--color-white);
  margin: 0;
}

.button-wrapper:hover .button-extern {
  width: 150px;
  height: 150px;
}

.button-wrapper:hover .button-intern {
  width: 172px;
  height: 172px;
} */
</style>
