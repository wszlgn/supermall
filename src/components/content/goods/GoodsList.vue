<template>
  <div class="goods">
    <!-- <goods-list-item v-for="item in goods" :key="item.page" :goods-item="item"/> -->
    <ul>
      <li>1列表</li>
      <li>2列表</li>
      <li>3列表</li>
      <li>4列表</li>
      <li>5列表</li>
      <li>6列表</li>
      <li>7列表</li>
      <li>8列表</li>
      <li>9列表</li>
      <li>10列表</li>
    </ul>
  </div>
</template>

<script>
  import GoodsListItem from './GoodsListItem'

  export default {
    name: "GoodsList",
    components: {
      GoodsListItem
    },
    props: {
      goods: {
        type: Array,
        default() {
          return []
        }
      }
    }
  }
</script>

<style scoped>
  .goods {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;

    padding: 2px;
  }


</style>
