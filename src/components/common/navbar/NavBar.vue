<template>
  <div class="nav-bar">
    <div class="left"><slot name="left"></slot></div>
    <div class="center"><slot name="center"></slot></div>
    <div class="right"><slot name="right"></slot></div>
  </div>
</template>

<script>
  export default {
    name: 'NavBar'
  }
</script>

<style lang="scss" scoped>
.nav-bar{
  position: relative;
  display: flex;
  // width: 100%;
  height: 44px;
  line-height: 44px;
  text-align: center;
  box-shadow: 0 1px 1px rgba(100,100,100,.1);
  z-index: 10;
}
.left .right{
  width: 60px;
  background-color: aqua;
}
.center{
  flex: 1;
}
</style>