<template>
  <div class="MainNav-Mine-main">
   <div class="limit">
      <!-- 我的--上部 -->
    <div class="minetop">
      <!-- 用户信息 -->
      <div class="user">苏江穗</div>
      <!-- 我的 列表 -->
      <div class="minetop-nav">
        <ul class="minetopnavlist">
          <li v-for="(item,index) in minetopnavlist" :key="index">{{item}}</li>
        </ul>
      </div>
    </div>
    <!-- 我的--下部 -->
    <div class="minebottom">
      <div class="mymusic">我的音乐</div>
      <div class="zjplay">最近播放</div>
      <div class="musiclist">创建歌单</div>
    </div>
   </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      minetopnavlist: [
        "本地音乐",
        "下载管理",
        "我的电台",
        "我的收藏",
        "关注新歌",
      ],
    };
  },
};
</script>

<style scoped>
.MainNav-Mine-main {
  background: forestgreen;
}
.minetop{
  width: 100%;
  height: 45vh;
  background: yellowgreen;
  border: 1px solid transparent;
  box-sizing: border-box;
}
.user{
  width: 100%;
  height: 18vh;
  background: skyblue;
  margin-top: 10vh;
}
.minetop-nav{
  width: 100%;
  height: 17vh;
  background: turquoise;
}
.minetopnavlist{
  padding: 0;
  margin: 0;
}
.minetopnavlist>li{
  display: inline-block;
  list-style: none;
  width: 20%;
  height: 14vh;
  line-height: 9vh;
  text-align: center;
}
.minebottom{
  position: relative;
  top: -3vh;
  border: 1px solid transparent;
  box-sizing: border-box;
  width: 100%;
  border-top-left-radius: 3vh;
  border-top-right-radius: 3vh;
  background: white;
}
.mymusic{
  width: 100%;
  height: 27vh;
  margin-top: 3vh;
  background: yellow;
}
.zjplay{
  width: 100%;
  height: 18vh;
  margin-top: 3vh;
  background: tomato;
}
.musiclist{
  width: 100%;
  height: 30vh;
  margin-top: 3vh;
  background: teal;
}</style>