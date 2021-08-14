<template>
  <div id="home">

     <div class="wrap-nav"><nav-bar class="home-nav">
      <template v-slot:center>
        <div>购物车</div>
      </template>
    </nav-bar></div>
    <home-swiper :banners="banners" />
    <recommend-view :recommends="recommends" />
    <feature-view/>
    <tab-control class="tab-control" :titles="['流行', '新品', '精选']" />
    <goods-list />
    <ul>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
      <li>列表11</li>
      <li>列表12</li>
      <li>列表13</li>
      <li>列表14</li>
      <li>列表15</li>
      <li>列表16</li>
      <li>列表17</li>
      <li>列表18</li>
      <li>列表19</li>
      <li>列表20</li>
      <li>列表21</li>
      <li>列表22</li>
      <li>列表23</li>
      <li>列表24</li>
      <li>列表25</li>
      <li>列表26</li>
      <li>列表27</li>
      <li>列表28</li>
      <li>列表29</li>
      <li>列表30</li>



    </ul>
  </div>
</template>
<script>
import HomeSwiper from './childComps/HomeSwiper.vue';
import RecommendView from './childComps/RecommendView.vue'
import FeatureView from './childComps/featureView.vue'

import NavBar from "components/common/navbar/NavBar.vue";
import TabControl from  'components/content/tabControl/TabControl'
import GoodsList from 'components/content/goods/GoodsList.vue';
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
      }
    };
  },
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    getHomeGoods,
    GoodsList,
  },
  activated() {},
  watch: {},
  created() {
    // 1.请求多个数据
   this.getHomeMultidata();
    // 2.请求商品数据
   this.getHomeGoods('pop');

   this.getHomeGoods('new');

   this.getHomeGoods('sell');
  },
  methods: {
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
  })
    }
  }
}
</script>
<style scoped>
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
}
.wrap-nav {
  position: relative;
  height: 44px;
}
.tab-control {
  position: sticky;
  top: 44px;
}
</style>
