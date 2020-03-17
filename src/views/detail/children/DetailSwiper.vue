<template>
  <div class='detail-swiper'>
    <swiper class="swipers">
      <swiper-item  v-for="item in topImages" :key="item">
        <img :src="item" alt="">
      </swiper-item>
    </swiper>
  </div>
</template>

<script>
import {Swiper,SwiperItem} from "components/common/swiper"
export default {
  name: 'DetailSwiper',
  data(){
    return {}
  },
  props:{
    topImages:{
      type: Array,
      default(){
        return []
      }
    }
  },
  components: {
    Swiper,
    SwiperItem
  },
  created(){},
  mounted(){},
  methods: {}
}
</script>
<style lang='scss' scoped>
.swipers{
  height: 300px;
  overflow: hidden;
}
</style>
