<template>
    <div>
      <swiper>
      <swiper-item  v-for="item in banners" :key="item.title">
        <template v-slot:carousel>
          <a :href="item.link">
            <img :src="item.image" alt="">
          </a>
        </template>
      </swiper-item>
    </swiper>
    </div>
</template>
<script>
import { Swiper, SwiperItem } from "components/common/swiper";

export default {
  name: 'HomeSwiper',
    props: {
      banners: {
        type: Array,
        default() {
          return [];
        }
      }
  },
   data() {
      return {
      }
   },
   components: {
     Swiper,
     SwiperItem
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
</style>
