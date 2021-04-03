<template>
  <div  id="hy-swiper">
    <div class="swiper" @touchstart="touchstart" @touchmove="touchmove" @touchend="touchend">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "Swiper",
  data(){
    return{
      slideCount: 0, // 元素个数
      totalWidth: 0, // swiper的宽度
      swiperStyle: {}, // swiper样式
      currentIndex: 1, // 当前的index
      scrolling: false, // 是否正在滚动
    }
  },
  methods:{
    /**
     * 定时器操作
     */
    startTimer(){
      this.playTimer = window.setInterval(() => {
        this.currentIndex++;

      }, this.interval)
    },
    stopTimer(){
      window.clearInterval(this.playTimer)
    },
    touchstart(e){
      // 1.如果正在滚动, 不可以拖动
      if(this.scrolling) return;

      // 2.停止定时器
      this.stopTimer()

    }
  }
}
</script>

<style scoped>

</style>
