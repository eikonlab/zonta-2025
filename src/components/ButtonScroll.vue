<script setup></script>

<template>
  <div id="button-wrapper">
    <svg
      class="scroll-icon"
      xmlns="http://www.w3.org/2000/svg"
      width="73"
      height="73"
      viewBox="0 0 73 73"
      fill="none"
    >
      <circle class="pulse" cx="36.2715" cy="36.2715" r="35.7715" />
      <rect class="mouse" x="27.5" y="23.5" width="16.9915" height="26.4489" rx="8.49574" />
      <circle class="wheel" cx="35.9961" cy="31.5666" r="1.78317" />
    </svg>
    <p>Scrollez pour Explorer</p>
    <div id="line"></div>
  </div>
</template>

<style scoped>
#button-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

p {
  margin-top: 30px;
}

#line {
  width: 1.4px;
  height: 317px;
  opacity: 0.2;
  background-color: var(--color-white);
}

/* Animation souris */
.scroll-icon {
  overflow: visible;
}

.mouse {
  fill: none;
  stroke: white;
}

.wheel {
  fill: white;
  animation: wheelMove 4s infinite;
}

.pulse {
  fill: none;
  stroke: white;
  stroke-width: 1;
  opacity: 0;
  transform-origin: center;
  animation: pulse 4s infinite;
}

@keyframes wheelMove {
  0% {
    transform: translateY(0);
    opacity: 1;
  }

  40% {
    transform: translateY(9px);
    opacity: 1;
  }

  50% {
    transform: translateY(9px);
    opacity: 0;
  }

  51% {
    transform: translateY(-4px);
    opacity: 0;
  }

  70% {
    transform: translateY(0);
    opacity: 1;
  }

  100% {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes pulse {
  0% {
    transform: scale(0.8);
    opacity: 0;
  }

  40% {
    transform: scale(1);
    opacity: 0;
  }

  50% {
    transform: scale(1);
    opacity: 0.7;
  }

  80% {
    transform: scale(1.6);
    opacity: 0;
  }

  100% {
    transform: scale(1.6);
    opacity: 0;
  }
}
</style>
