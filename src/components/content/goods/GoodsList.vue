<template>
  <div class="goods">
   <goods-list-item v-for="(item,index) in goods" :key="index" :goods-item="item" />
   <!-- {{goods}} -->
  </div>
</template>

<script>
import GoodsListItem from './GoodsListItem'
  export default {
    name: 'GoodsList',
    props: {
      goods:{
        type: Array,
        default() {
          return [];
        }
      }
    },
    components: {
      GoodsListItem // 商品item
    }
  }
</script>

<style lang="scss" scoped>
  .goods {
    display: flex;
    flex-wrap: wrap; //默认是不包裹
    justify-content: space-around;

    padding: 2px;
  }
</style>