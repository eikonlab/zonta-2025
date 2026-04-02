<script setup>
import ButtonScroll from './../components/ButtonScroll.vue'
import { onMounted, ref } from 'vue'

const ScrollerRef = ref(null)
const scrollPosition = ref(0)
const emit = defineEmits(['jumpToStats'])
const blockScroll = ref(false)

const handleScroll = () => {
  if (ScrollerRef.value) {
    const scroller = ScrollerRef.value
    const scrollPercentage =
      (scroller.scrollTop / (scroller.scrollHeight - scroller.clientHeight)) * 100
    scrollPosition.value = scrollPercentage
    console.log('Scroll position:', scrollPosition.value + '%')
    if (scrollPercentage >= 99 && !blockScroll.value) {
      emit('jumpToStats')
      blockScroll.value = true
    }
  }
}

onMounted(() => {
  const scroller = ScrollerRef.value
  if (scroller) {
    scroller.addEventListener('scroll', handleScroll)

    return () => {
      scroller.removeEventListener('scroll', handleScroll)
    }
  }
})
</script>

<template>
  <div id="scroller" ref="ScrollerRef">
    <div id="intro-scroll">
      <div id="intro-scroll-position-button-scroll">
        <div id="intro-scroll-button-parent">
          <div id="intro-scroll-button-div">
            <ButtonScroll :scrollValue="scrollPosition"></ButtonScroll>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
#scroller {
  height: 100vh;
  width: 100%;
  overflow-y: scroll;
  scrollbar-width: none;
}

#scroller::-webkit-scrollbar {
  display: none;
}

#intro-scroll-button-parent {
  width: 100%;
  height: 100vh;
}

#intro-scroll-button-div {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}

#intro-scroll-position-button-scroll {
  width: 100%;
  height: 100vh;
  inset: 0;
  position: sticky;
}

#intro-scroll {
  position: relative;
  height: 200vh !important;
}
</style>
