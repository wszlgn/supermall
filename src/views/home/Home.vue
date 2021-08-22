<template>
  <div id="home">
    <div class="wrap-nav">
    <div class="nav-height"><nav-bar class="home-nav">
      <template v-slot:center>
        <div>购物车</div>
      </template>
    </nav-bar>
    </div>
    </div>
    <scroll class="content" ref="scroll"
    v-bind:probe-type="3"
    v-bind:pull-up-load="true"
    v-on:scroll="contentScroll"
    v-on:pullingUp="loadMore" >
      <template v-slot:roll>
        <home-swiper v-bind:banners="banners" />
        <recommend-view v-bind:recommends="recommends" />
        <feature-view/>
        <tab-control class="tab-control" v-bind:titles="['流行', '新品', '精选']"
        @tabClick='tabClick' />
        <goods-list v-bind:goods="showGoods" />
      </template>
    </scroll>
    <back-top v-on:click.native="btnClick" v-show="isShowBackTop" />
  </div>
</template>
<script>
import HomeSwiper from './childComps/HomeSwiper.vue';
import RecommendView from './childComps/RecommendView.vue'
import FeatureView from './childComps/featureView.vue'

import NavBar from "components/common/navbar/NavBar.vue";
import TabControl from  'components/content/tabControl/TabControl'
import GoodsList from 'components/content/goods/GoodsList.vue';
import Scroll from 'components/common/scroll/Scroll.vue'
import BackTop from 'components/content/backTop/BackTop.vue'

import { getHomeMultidata, getHomeGoods } from "network/home.js";

export default {
  name: "Home",
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': {page: 0, list: []},
        'new': {page: 0, list: []},
        'sell': {page: 0, list: []},
      },
      currentType: 'pop',
      isShowBackTop: false,
    };
  },
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList,
    Scroll,
    BackTop,
  },
  activated() {},
  created() {
    // 1.请求多个数据
   this.getHomeMultidata();
    // 2.请求商品数据
   this.getHomeGoods('pop');

   this.getHomeGoods('new');

   this.getHomeGoods('sell');
  },
  methods: {
    btnClick() {
      this.$refs.scroll.scrollTo(0, 0)
    },
    /**
     *  事件监听相关的方法
     */
  tabClick(index) {
    switch (index) {
      case 0:
        this.currentType = 'pop'
        break;
      case 1:
        this.currentType = 'new'
        break;
      case 2:
        this.currentType = 'sell'
        break;
    }
  },
    /**
     *  网络请求相关的方法
     */
    getHomeMultidata() {
    getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
  },
    getHomeGoods(type) {
      const page = this.goods[type].page +1;
      getHomeGoods(type , page).then(res => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;

        this.$refs.scroll.finishPullUp();
  })
    },
    contentScroll(position) {
      this.isShowBackTop = (-position) > 1000
    },
    loadMore() {
      this.getHomeGoods (this.currentType);
      this.$refs.scroll.scroll.refresh();
    }
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    },

}
}
</script>
<style scoped>
#home {
  position: relative;
  height: 100vh;
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}
.nav-height {
  height: 44px;
}
.wrap-nav {
  position: relative;
  height: 44px;
}
.tab-control {
  position: sticky;
  top: 44px;
  z-index: 9;
}
.content {
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
  overflow: hidden;
}
</style>
