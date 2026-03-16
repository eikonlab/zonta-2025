<script setup></script>

<template>
  <div id="timeline-wrapper">
    <p>Test</p>
    <p>Test</p>
  </div>
</template>

<style scoped>
#timeline-wrapper {
  background: red;
  width: 230px;
  height: 100vh;
  padding: 10px 18px;

  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.burger-layout {
  display: flex;
  flex-direction: column;
  justify-content: center;

  pointer-events: none;
  transition: background-color 0.3s ease;
}

/* Menu ouvert */
.menu {
  position: relative;
}

.burger-layout {
  transform: translateX(100%);
  opacity: 0;
  transition: all 0.3s ease;
  will-change: transform;
}

.burger-layout:has(.menu.is-active) {
  background-color: var(--color-white);
  pointer-events: auto;
  transform: translateX(0);
  opacity: 1;
}
</style>
