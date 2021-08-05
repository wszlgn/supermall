<template>
    <div id="recommend">
      <div  v-for="item in recommends" :key="item.title" class="recommend-item">
        <a :href="item.link">
          <img :src="item.image" alt="">
          <div>{{item.title}}</div>
        </a>
      </div>
    </div>
</template>
<script>
export default {
   name: 'RecommendView',
   props: {
     recommends: {
       type: Array,
       default() {
         return []
       }
     }
   },
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
<style scoped>
#recommend {
  display: flex;
  width: 100%;
  text-align: center;
  font-size: 12px;
  padding: 15px 0 30px;
  border-bottom: 8px solid #eee;
}
#recommend .recommend-item {
  flex: 1;
}
.recommend-item a img {
  width: 60px;
  height: 60px;
}
</style>
