<template>
  <div
    class="detphOfField"
    @mouseenter="mouseenterEvent"
    @mouseout="mouseoutEvent"
    @mousemove="mousemoveEvent"
    >
    <div>
      <img
        src="../assets/images/bilibili-autumn-1.webp"
        :style="`transform: translatex(${animationArr[0].offset}px);filter: blur(${animationArr[0].blurValue}px);`"
      >
    </div>
    <div>
      <img
        src="../assets/images/bilibili-autumn-2.webp"
        :style="`transform: translatex(${animationArr[1].offset}px);filter: blur(${animationArr[1].blurValue}px);`"
      >
    </div>
    <div>
      <img
        src="../assets/images/bilibili-autumn-3.webp"
        :style="`transform: translatex(${animationArr[2].offset}px);filter: blur(${animationArr[2].blurValue}px);`"
      >
    </div>
    <div>
      <img
        src="../assets/images/bilibili-autumn-4.webp"
        :style="`transform: translatex(${animationArr[3].offset}px);filter: blur(${animationArr[3].blurValue}px);`"
      >
    </div>
    <div>
      <img
        src="../assets/images/bilibili-autumn-5.webp"
        :style="`transform: translatex(${animationArr[4].offset}px);filter: blur(${animationArr[4].blurValue}px);`"
      >
    </div>
    <div>
      <img
        src="../assets/images/bilibili-autumn-6.webp"
        :style="`transform: translatex(${animationArr[5].offset}px);filter: blur(${animationArr[5].blurValue}px);`"
      >
    </div>
  </div>
</template>

<script>
import { ref, reactive } from 'vue'
export default {
  name: 'One',

  setup() {
    let startCoordinate = 0
    let endCoordinate = 0
    const percentage = ref(0)
    const animationArr = reactive({
      0: {
        offset: 0,
        blurValue: 0
      },
      1: {
        offset: 0,
        blurValue: 0
      },
      2: {
        offset: 0,
        blurValue: 0
      },
      3: {
        offset: 0,
        blurValue: 0
      },
      4: {
        offset: 0,
        blurValue: 3
      },
      5: {
        offset: 0,
        blurValue: 3
      }
    })
    const mouseenterEvent = (e) => {
      startCoordinate = e.clientX;
      percentage.value = e.clientX / window.outerWidth
    }

    const mousemoveEvent = (e) => {
      animationFyn(e.clientX)
    }
    const mouseoutEvent = (e) => {
      endCoordinate = e.clientX;
      let time = setInterval(() => {
        endCoordinate = endCoordinate < startCoordinate ? startCoordinate : endCoordinate - 35
        animationFyn(endCoordinate)
        if (endCoordinate === startCoordinate) {
          clearInterval(time)
        }
      }, 10)
    }

    function animationFyn (clientX) {
      percentage.value = clientX / window.outerWidth
      let offset = 10 * percentage.value
      let blur = 7
      for(let i = 0; i < 6; i++){
        offset *= 1.2
        animationArr[i].offset = offset
        animationArr[i].blurValue = (Math.pow((i / 5 - percentage.value ), 2) * blur)
      }
    }

    return {
      mouseenterEvent,
      mouseoutEvent,
      mousemoveEvent,
      animationArr
    }
  }
}
</script>

<style scoped>
.detphOfField {
  position: relative;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  min-height: 155px;
  overflow: hidden
}
.detphOfField div {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

}
.detphOfField div img {
  display: block;
  width: 110%;
  height: 100%;
  object-fit: cover;
}
</style>
