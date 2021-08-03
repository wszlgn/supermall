<template>
        <div class="tar-bar-item" @click='itemClick'>
            <div  v-if="!isActive"><slot name="item-icon"></slot></div>
            <div v-else><slot  name="item-icon-active"></slot></div>
           <div :class="{active: isActive}"><slot  name= "item-text"></slot></div> 
        </div>
</template>
<script>
// import {debounce} from '../../debounce'
export default {
    name: 'TabBarItem',
   data() {
      return {
      }
   },
   props: {
       path: String,
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
    itemClick() {
        this.$router.push(this.path);
    }
},
computed: {
    isActive() {
        return this.$route.path.indexOf(this.path) !== -1; // 可以判断活跃状态
    }
}
}
</script>
<style>
#tar-bar {
    display: flex;
    background-color: #f6f6f6;
    position: fixed;
    left: 0;
    bottom: 0;
    right: 0;
    box-shadow: 0 0.1px 1px rgba(150, 150, 300, 1);
}

.tar-bar-item {
    flex: 1;
    height: 49px;
    text-align: center;
    font-size: 14px;
}
.tar-bar-item img {
    width: 24px;
    height: 24px;
    margin-top: 3px;
    margin-bottom: 2px;
    vertical-align: middle;
}
.active {
    color: lightcoral;
}
</style>
