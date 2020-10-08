<template>
  <div class="MainNav-Icould-main">
    <div class="limit">
      <!-- 音乐盒子 -->
      <div class="music-nav">
        <!-- 推荐音乐 -->
        <a @click="change">
          <div class="tab-title">
            <div class="tab-txt" :class="{choose:!isshow}">
              <span>推荐音乐</span>
            </div>
          </div>
        </a>
        <!-- 热歌榜 -->
        <a @click="change">
          <div class="tab-title">
            <div class="tab-txt" :class="{choose:isshow}">
              <span>热歌榜</span>
            </div>
          </div>
        </a>
      </div>
      <!-- 主体 -->
      <div class="main-content">
        <!-- 推荐音乐模块 -->
        <Recommend :class="{show:isshow}"></Recommend>
        <!-- 热歌榜模块 -->
        <HotMusic :class="{show:!isshow}"></HotMusic>
      </div>

      <!-- 底部播放模块 -->
      <MainPlay></MainPlay>
    </div>
  </div>
</template>

<script>
import Recommend from "../musicplay/Recommend";
import HotMusic from "../musicplay/HotMusic";

import MainPlay from '../MainPlay'

// import transmitmusicinfo from 

export default {
  components: {
    Recommend,
    HotMusic,
    MainPlay
  },
  data(){
    return{
      isshow:false
    }
  },
  methods:{
    change:function(){
      this.isshow = !this.isshow
      // console.log(this)
    }
  },
};
</script>

<style scoped>
.MainNav-Icould-main {
  background: white;
}
.music-nav {
  width: 100vw;
  position: fixed;
  top: 10vh;
  background: rgb(251, 253, 253);
  z-index: 20;
  box-shadow: 10px 1px gainsboro
}
.tab-title {
  width: 50%;
  height: 100%;
  /* background: chartreuse; */
  float: left;
  text-align: center;
}
.tab-txt {
  position: relative;
  display: inline-block;
  max-width: 100%;
  height: 100%;
  padding: 0 5px;
  box-sizing: border-box;
  color: #333;
  font-size: 15px;
  line-height: 40px;
  /* background: red; */
}
.tab {
  width: 100vw;
  position: relative;
  top: calc(10vh + 40px);
  overflow-x: hidden;
  overflow-y: scroll;
}
.show{
  display: none;
}
.choose{
  border-bottom: 1px solid red;
  box-sizing: border-box;
  color: red;
}
</style>