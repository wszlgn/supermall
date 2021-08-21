<template>
    <div class="wrapper" ref="wrapper">
      <dir class="content">
        <slot name="roll"></slot>
      </dir>
    </div>
</template>
<script>
import BScroll from 'better-scroll'
export default {
name: 'Scroll',
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
  this.scroll = new BScroll(this.$refs.wrapper, {
  })
},
methods:{
}


}
</script>
<style>

</style>
