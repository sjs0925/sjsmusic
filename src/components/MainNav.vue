<template>
  <!-- 顶部界面切换模块 -->
  <div class="MainNav-main">
    <!-- 菜单 -->
    <div class="frist" @click="choosemenu">菜单</div>
    <!-- 模块列表 -->
    <ul class="topnav">
      <li class="navcontent" v-for="(item,index) in menulist"
       :key="index" @click="chooselist(index)" 
       :class="choose == index?'choose':''">{{item}}</li>
    </ul>
    <!-- 搜索 -->
    <div class="last" @click="choosesearch">
      <img class="searchimg" src="../assets/Images/zoom.png" alt="">
    </div>
  </div>
</template>

<script>
import transmit from '../assets/new'

export default {
  data() {
    return {
      menulist: ["我的", "发现", "悦听", "视频"],
      leftnum: "0vw",
      choose:2
    };
  },
  props: ["activemenu", "activesearch"],
  methods: {
    choosemenu: function () {
      this.$parent.showmenu();
    },
    choosesearch: function () {
      this.$parent.showsearch();
    },
    chooselist: function (index) {
      this.choose = index;
      // alert('别点了,这是还没打完的江山');
      transmit.$emit('transmitindex',index);
    },
  }
};
</script>

<style scoped>
.MainNav-main {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 10vh;
  font-size: large;
  background: rgb(255, 255, 255);
  /* background: gold; */
  /* opacity: 0.2; */
  z-index: 30;
  display: flex;
  z-index: 25;
}
.MainNav-main::after{
       content: '';
    position: absolute;
    width: 100%;
    height: 1px;
    background: rgb(220, 220, 200);
    bottom:0;
    left: 0;
}
.frist,
.last {
  width: 15vw;
  align-items: center;
  line-height: 10vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
.topnav {
  width: 70vw;
  align-items: center;
  text-align: center;
  padding: 0;
  margin: 0;
}
.navcontent {
  display: inline-block;
  list-style: none;
  width: 22%;
  line-height: 10vh;
  font-size: 16px;
    color: darkgray;
}
.choose,#choose{
  font-size: 20px;
  color: #333;
}
.last {
  text-align: right;
}
.searchimg{
  width: 30%;
}
</style>