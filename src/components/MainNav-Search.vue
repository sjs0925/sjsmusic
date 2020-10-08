<template>
  <div class="MainNav-Search-main">
    <div class="search-content">
      <!-- 搜索 输入 -->
      <div class="search">
        <!--  返回 -->
        <div class="back" @click="ycSearch">back</div>
        <!-- 输入框 -->
        <div class="search-input" @keyup.enter="change">
          <input
            class="userinput"
            type="text"
            autofocus="autofocus"
            placeholder="请输入"
            v-model="keymusicname"
          />
        </div>
        <!-- search -->
        <div class="search-click" @click="change">
          <!-- <img class="search-img" src="../assets/Images/zoom.png" alt=""> -->
        </div>
      </div>
      <!-- 搜索 推荐 -->

      <!-- 搜索 列表 -->
      <!-- 搜索 播放 -->
      <!-- <MainPlay v-show="isshow"></MainPlay> -->
    </div>
  </div>
</template>

<script>
import MainPlay from "./MainPlay";

export default {
  components: {
    MainPlay,
  },
  props: ["activesearch"],
  data() {
    return {
      bpxnum: false,
      keymusicname: "",
      searchmusivinfo: [],
    };
  },
  methods: {
    ycSearch() {
      this.$parent.ycsearch();
    },
    //搜索
    change() {
      if (this.keymusicname == "") return;
      axios
        .get(
          "https://autumnfish.cn/search?keywords=" +
            this.keymusicname +
            "&limit=50"
        )
        .then((response) => {
        //   console.log(response);

          for (let i = 0; i < 30; i++) {
            const data = {};

            //获取歌曲id
            data.smid = response.data.result.songs[i].id;
            //歌名
            data.smname = response.data.result.songs[i].name;
            //专辑
            data.smalbum = response.data.result.songs[i].album.name;
            axios.get("https://autumnfish.cn/song/detail?ids=" + data.smid).then((response) => {data.smimg = response.data.songs[0].al.picUrl;});
            axios.get("https://autumnfish.cn/song/url?id=" + data.smid).then((response) => {data.smurl = response.data.data[0].url;});
            this.searchmusivinfo.push(data);
          }
        });
    },
  },
};
</script>

<style scoped>
.MainNav-Search-main {
  position: fixed;
  top: 100vh;
  width: 100vw;
  height: 180vh;
  background: linear-gradient(to bottom, yellow, blue);
  z-index: 40;
  transition: top 0.1s;
  overflow-y: scroll;
}
.showsearch {
  top: 0;
}
.search {
  width: 100vw;
  height: 60px;
  background: white;
  display: flex;
  justify-content: center;
  /* position: fixed; */
  top: 0;
}
.back {
  width: 15%;
  text-align: center;
  line-height: 60px;
  position: relative;
  /* background: red; */
}
.back::after {
  content: "";
  width: 1px;
  height: 44px;
  position: absolute;
  right: 0;
  top: 8px;
  background: rgb(230, 230, 230);
}
.search-input {
  width: 70%;
  height: 60px;
  border-bottom: 1px solid gray;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  background: white;
}
.userinput {
  width: 100%;
  height: 42px;
  border: none;
  line-height: 42px;
  text-indent: 10px;
  font-size: larger;
  color: gray;
  outline: none;
}
.search-click {
  position: relative;
  width: 15%;
  /* height: 60px; */
  display: flex;
  /* align-content: center; */
  /* justify-content: center; */
  background: url(../assets/Images/zoom.png) no-repeat;
  background-position: center;
  /* background-color: blue; */
}
.search-click::before {
  content: "";
  position: absolute;
  top: 8px;
  left: 0;

  width: 1px;
  height: 44px;
  background: rgb(230, 230, 230);
}
</style>