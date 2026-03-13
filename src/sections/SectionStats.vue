<script setup>
import Statistics from './../parts/StatsStatistics.vue'
import HighlightedMessage from './../parts/StatsHighlightedMessage.vue'
import RecurringMessages from './../parts/StatsRecurringMessages.vue'
import AllMessages from './../parts/StatsAllMessages.vue'
</script>

<template>
  <div id="burger-recapitulatif">
    <Statistics></Statistics>

    <HighlightedMessage></HighlightedMessage>

    <RecurringMessages></RecurringMessages>

    <AllMessages></AllMessages>
  </div>
</template>

<style scoped></style>
