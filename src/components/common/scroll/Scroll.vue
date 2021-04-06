<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from '@better-scroll/core'
import PullUp from '@better-scroll/pull-up'

BScroll.use(PullUp)
export default {
  name: "Scroll",
  props:{
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      scroll: null
    }
  },
  mounted() {
    // 1.创建BScroll对象
    setTimeout(() => {
      if(!this.scroll){

        this.scroll = new BScroll(this.$refs.wrapper,{
          click: true,
          probeType: this.probeType,
          pullUpLoad: this.pullUpLoad
        });
        //  2.监听滚动的位置
        this.scroll.on('scroll', (position) => {
          this.$emit('scroll', position)
        })
      //  3.监听上拉事件
        this.scroll.on('pullingUp', () => {
          this.$emit('pullingUp')

          setTimeout(() => {
            this.scroll.finishPullUp();
            this.scroll.refresh()
          },300)

        })
      }else {
        this.scroll.refresh();
      }
    }, 500)
  },
  methods:{
    scrollTo(x, y, time = 300){
      this.scroll.scrollTo(x, y, time)
    }
  }

}
</script>

<style scoped>

</style>
