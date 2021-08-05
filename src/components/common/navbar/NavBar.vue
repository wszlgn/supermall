<template>
    <div class="nav-bar">
        <div class="left"><slot name="left"></slot></div>
        <div class="center"><slot name="center"></slot></div>
        <div class="right"><slot name="right" ></slot></div>
    </div>
</template>
<script>
export default {
    name: "NavBar",
   data() {
      return {
      }
   },
   activated() {
   },
 watch: {
},
created(){
},
mounted(){
},
methods:{
}


}
</script>
<style>
    .nav-bar {
        display: flex;
        text-align: center;
        height: 44px;
        line-height: 44px;
        box-shadow: 1 1 2 .1;
    }
    .left,
    .right {
        width: 60px;
    }

    .center {
        flex: 1;
    }
</style>
