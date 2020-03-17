<template>
  <div class='detail'>
    <detail-nav-bar class="detail-nav"></detail-nav-bar>
    <scroll class="contnet" ref="scroll">
      <div>
      <detail-swiper :top-images="topImage"></detail-swiper>
    <detail-base-info :goods="goods"></detail-base-info>
    <detail-shop-info :shop="shop"></detail-shop-info>
    <detail-goods-info :detail-info='detailInfo' @imageLoad="imageLoad"></detail-goods-info>
    <detail-param-info :param-info="paramInfo"></detail-param-info>
    </div>
    </scroll>
  </div>
</template>

<script>
import DetailNavBar from "./children/DetailNavBar"
import DetailSwiper from "./children/DetailSwiper"
import DetailBaseInfo from "./children/DetailBaseInfo"
import DetailShopInfo from "./children/DetailShopInfo"
import DetailGoodsInfo from "./children/DetailGoodsInfo"
import DetailParamInfo from "./children/DetailParamInfo"

import Scroll from "components/common/scroll/Scroll"
import {getDetail,Goods,shop,GoodsParam} from "network/detail"
export default {
  name: 'detail',
  data(){
    return {
      iid:null,
      topImage:[],
      // 三种数据
      goods:{},
      // 商家信息
      shop: {},
      // 商品详细信息
      detailInfo:{},
      // 参数信息
      paramInfo:{},
    }
  },
  components: {
    DetailNavBar,
    DetailSwiper,
    // 第二栏
    DetailBaseInfo,
    // 店铺信息
    DetailShopInfo,
    Scroll,
    DetailGoodsInfo,
    // 参数组件
    DetailParamInfo
  },
  created(){
    // 1. 保存传入的iid
    this.iid = this.$route.params.iid
    // 2. 根据iid请求详细数据
    getDetail(this.iid).then(res=>{
      // 封装一下数据
      const data =  res.result;
      console.log(res)
      // 1. 获取顶部的图片轮播数据
      this.topImage = data.itemInfo.topImages;

      // 2. 获取商品信息
      this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services);
      // 3. 获取商家店铺信息
      this.shop = new shop(data.shopInfo);
      // 4. 保存商品详情数据
      this.detailInfo = data.detailInfo;
      // 5. 获取参数数据
      this.paramInfo = new GoodsParam(data.itemParams.info,data.itemParams.rule);
    })
  },
  mounted(){},
  methods: {
    imageLoad(){
      this.$refs.scroll.refresh();
    }
  }
}
</script>
<style lang='scss' scoped>
.detail{
  position: relative;
  z-index: 13;
  background-color: #fff;
  height: 100vh;
}
.contnet{
  // height: calc(100%-44px);
  // position: absolute;

  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;

}
.detail-nav{
  position: relative;
  z-index: 13;
  background-color: #fff;
}
</style>
