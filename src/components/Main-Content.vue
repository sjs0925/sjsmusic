<template>
  <div class="MainContent-main">
    <!-- 我的模块 -->
    <MainNavMine class="content-nav" :style="{left:leftnum}"></MainNavMine>
    <!-- 发现模块 -->
    <MainNavFine class="content-nav" :style="{left:leftnum}"></MainNavFine>
    <!-- 悦听模块 -->
    <MainNavIcould class="content-nav" :style="{left:leftnum}"></MainNavIcould>
    <!-- 视频模块 -->
    <MainNavMovie class="content-nav" :style="{left:leftnum}"></MainNavMovie>
  </div>
</template>

<script>
import transmit from '../assets/new'

import MainNavMine from "./mainnav/MainNav-Mine";
import MainNavFine from "./mainnav/MainNav-Fine";
import MainNavIcould from "./mainnav/MainNav-Icould";
import MainNavMovie from "./mainnav/MainNav-Movie";

export default {
  components: {
    MainNavMine,
    MainNavFine,
    MainNavIcould,
    MainNavMovie,
  },
  data(){
    return{
      leftnum:'-200vw'
    }
  },
  created(){
    transmit.$on('transmitindex',index => {
      this.leftnum = -index + '00vw';
      // console.log(this.leftnum);
    })
  }
};
</script>

<style scoped>
.MainContent-main {
  display: flex;
  overflow-x: hidden;
  overflow-y: scroll;
  position: relative;
}
.content-nav {
  width: 100vw;
  height: 100vh;
  align-items: center;
  position: relative;
  /* left: -200vw; */
  float: left;
  transition: left 0.1s;
}
</style>