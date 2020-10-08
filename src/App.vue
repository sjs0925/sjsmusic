<template>
  <div id="app">
      <!-- 界面模块--主体 -->
      <MainContent></MainContent>
      <!-- 界面模块--菜单 设置 -->
      <MainNavMenu :class="{showmenu:isshowmenu}" :activemenu="ycmenu"></MainNavMenu>
      <!-- 界面模块--搜索 -->
      <MainNavSearch :class="{showsearch:isshowsearch}" :activesearch="ycsearch"></MainNavSearch>
      <!-- 顶部界面切换模块 -->
      <MainNav :activemenu="showmenu" :activesearch="showsearch"></MainNav>
      <!-- 播放模块 -->
      <!-- <MainPlay></MainPlay> -->

  </div>
</template>

<script>
import MainNav from "./components/MainNav"
import MainPlay from './components/MainPlay'

import MainNavMenu from './components/MainNav-Menu'
import MainNavSearch from './components/MainNav-Search'

import MainContent from './components/Main-Content'

export default {
  name: "App",
  components: {
    MainNav,
    MainPlay,
    MainNavMenu,
    MainNavSearch,
    MainContent
  },
  data(){
    return{
      isshowmenu:false,
      isshowsearch:false,
    }
  },
  methods:{
    showmenu:function(){
      this.isshowmenu = !this.isshowmenu
    },
    ycmenu:function(){
      this.isshowmenu = !this.isshowmenu
    },
    showsearch:function(){
      this.isshowsearch = !this.isshowsearch
    },
    ycsearch:function(){
      this.isshowsearch = !this.isshowsearch
    }
  },
  
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  padding: 0;
}
* {
  padding: 0px;
  margin: 0px;
}
.limit{
  width: 100vw;
  height: 100vh;
  overflow-y: scroll;
}
a {
  text-decoration: none;
  color: black;
}
.text {
  position: relative;
  padding-left: 9px;
  margin-bottom: 14px;
  font-size: 17px;
  height: 20px;
  line-height: 20px;
  /* background: skyblue; */
  /* background: red; */
}
.text::after {
  content: "";
  position: absolute;
  left: 0;
  top: 50%;
  margin-top: -9px;
  width: 3px;
  height: 16px;
  background-color: #d33a31;
}
</style>
