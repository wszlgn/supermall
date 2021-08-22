<template>
    <div class="wrapper" ref="wrapper">
      <div class="content">
        <slot name="roll"></slot>
      </div>
    </div>
</template>
<script>
import BScroll from 'better-scroll'
export default {
name: 'Scroll',
props: {
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
        scroll: null,
  }
   },
   activated() {
   },
 watch: {
},
created(){

},
mounted(){
  /**
   *  1.创建 BScroll 对象
   */
  this.scroll = new BScroll(this.$refs.wrapper, {
    click: true,
    probeType: this.probeType,
    pullUpLoad: this.pullUpLoad,
  });
  /**
   *  2.监听 BScroll 对象
   */
  this.scroll.on('scroll', (position) => {
      this.$emit('scroll', position)
  })
  this.scroll.on('pullingUp', () => {
      this.$emit('pullingUp')
  } )
},
methods:{
  scrollTo(x, y, time=500) {
    this.scroll.scrollTo(x, y, time);
  },
  finishPullUp() {
    this.scroll.finishPullUp()
  }
}


}
</script>
<style>

</style>
