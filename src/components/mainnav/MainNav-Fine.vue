<template>
  <div class="MainNav-Fine-main">
    <div class="limit">
      <!-- 发现 上部 -->
    <div class="finetop">
      <!-- 轮播 -->
      <div class="ratotionimg">
          
      </div>
      <!-- 发现列表 -->
      <div class="finenav">
        <ul>
          <li v-for="(item,index) in finelist" :key="index">
            <!-- {{item}} -->
          </li>
        </ul>
      </div>
    </div>
    <!-- 发现 下部 -->
    <div class="bottom">
    </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      ratotionimglist:['../../assets/1.jpg','../../assets/2.jpg','../../assets/3.jpg','../../assets/4.jpg','../../assets/5.jpg'],
      finelist:['每日推荐','歌单','排行榜','直播','电台','火前留名','数字专辑','唱聊','游戏专区','新说唱','线上演出'],
      defaultindex:0,//默认显示图片
      timer:null //定时器
    }
  }
}
</script>

<style scoped>
.MainNav-Fine-main {
  background: red;
}
.finetop{
  word-wrap: 100vw;
  height: 57vh;
  background: thistle;
  border: 1px solid transparent;

}
.ratotionimg{
  width: 100vw;
  height: 30vh;
  margin-top: 10vh;
  background: turquoise;
}
.finenav{
  width: 100vw;
  height: 14vh;
  margin-top: 3vh;
  background: wheat;
}
</style>