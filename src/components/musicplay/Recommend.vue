<template>
  <div class="recommend-main">
    <!-- 推荐音乐内容 -->
    <div class="tab recommend-content">
      <h2 class="text">推荐歌单</h2>
      <div class="remd-songs">
        <div class="remd-ul">
          <a class="remd-li" href="//y.music.163.com/m/playlist?id=5217031096">
            <div class="remd-img">
              <img src="../../assets/Icould/1.jpg" alt class="list-img" />
            </div>
            <p class="remd-text">JAZZ | 咖啡重度依赖者必备</p>
          </a>
          <a class="remd-li" href="//y.music.163.com/m/playlist?id=5166833101">
            <div class="remd-img">
              <img src="../../assets/Icould/2.jpg" alt class="list-img" />
            </div>
            <p class="remd-text">关于“我爱你”的四十种表达方式</p>
          </a>
          <a class="remd-li" href="//y.music.163.com/m/playlist?id=4988043536">
            <div class="remd-img">
              <img src="../../assets/Icould/3.jpg" alt class="list-img" />
            </div>
            <p class="remd-text">你的眼里只有星星却没有我</p>
          </a>
          <a class="remd-li" href="//y.music.163.com/m/playlist?id=5164757846">
            <div class="remd-img">
              <img src="../../assets/Icould/4.jpg" alt class="list-img" />
            </div>
            <p class="remd-text">流行歌手Gulgine</p>
          </a>
          <a class="remd-li" href="//y.music.163.com/m/playlist?id=5146965725">
            <div class="remd-img">
              <img src="../../assets/Icould/5.jpg" alt class="list-img" />
            </div>
            <p class="remd-text">你-总是有各种理由让我放弃你☹</p>
          </a>
          <a class="remd-li" href="//y.music.163.com/m/playlist?id=5002317855">
            <div class="remd-img">
              <img src="../../assets/Icould/6.jpg" alt class="list-img" />
            </div>
            <p class="remd-text">爱上你，需要踏遍山河的勇气</p>
          </a>
        </div>
      </div>
    </div>
    <!-- 新歌榜内容 -->
    <div class="tab newmusic-content">
      <h2 class="text">最新音乐</h2>
      <div class="new-songs">
        <div class="songs-ul">
          <a
            href="javascript:;"
            class="songs-li"
            v-for="(item,index) in newsongsinfo"
            :key="index"
            @click="transmitnminfo(index)"
          >
            <div class="songs-play">
              <div class="spl">
                <div class="sptext spname">{{item.nmname}}</div>
                <div class="sptext spinfo">{{item.nmsonger}} - {{item.nmalbum}}</div>
              </div>
              <div class="spr">
                <span class="spr-img"></span>
              </div>
            </div>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import transmitnewmusicinfo from "../../assets/transmitnminfo";

export default {
  data() {
    return {
      //最新音乐 音乐信息
      newsongsinfo: [],
    };
  },
  methods: {
    //新歌速递
    shownewsongs() {
      //获取ID
      axios.get("https://autumnfish.cn/top/song?type=0").then((response) => {
        // console.log(response.data.data[3])
        // console.log(response);
        for (let i = 0; i < 10; i++) {
          const data = {};
          //填入歌曲名
          data.nmname = response.data.data[i].name;
          // 歌手
          data.nmsonger = response.data.data[i].artists[0].name;
          // 专辑
          data.nmalbum = response.data.data[i].album.name;
          // id
          data.nmid = response.data.data[i].privilege.id;
          //填入歌曲封面
          data.nmimg = response.data.data[i].album.blurPicUrl;
          // console.log(this.newsongsinfo)
          //填入URL
          axios
            .get("https://autumnfish.cn/song/url?id=" + data.nmid)
            .then((response) => {
              data.nmurl = response.data.data[0].url;
            });
          this.newsongsinfo.push(data);
        }
      });
    },
    transmitnminfo(index) {
      transmitnewmusicinfo.$emit(
        "transmitnewmusicinfo",
        this.newsongsinfo,
        index
      );
    },
  },

  created() {
    this.shownewsongs();
  },
};
</script>

<style scoped>
.recommend-main {
  width: 100vw;
  position: relative;
  top: calc(10vh + 40px);
  overflow-x: hidden;
  overflow-y: scroll;
}

.recommend-content {
  margin-top: 15px;
}
.remd-songs {
  width: 100vw;
  margin-top: 10px;
  /* background: blueviolet; */
}
.remd-ul {
  display: flex;
  flex-wrap: wrap;
}
.remd-li {
  padding-left: 0;
  padding-right: 2px;
  display: block;
  margin-bottom: 16px;
  float: left;
  width: 33.3%;
  box-sizing: border-box;
}
.remd-img {
  position: relative;
  padding-bottom: 100%;
}
.list-img {
  position: absolute;
  width: 100%;
  left: 0;
  top: 0;
  z-index: 1;
}
.remd-text {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  padding: 6px 2px 0 6px;
  min-height: 30px;
  line-height: 1.2;
  font-size: 13px;
}
.newmusic-content {
  width: 100vw;
  height: 50vh;
  margin-top: 15px;
  /* background: red; */
}
.new-songs {
  position: relative;
  min-width: 30px;
  margin-bottom: 10vh;
  /* background: yellow; */
}
.songs-ul {
  position: relative;
  /* display: flex; */
}
.songs-li {
  color: #333;
  display: flex;
  position: relative;
}
.songs-play {
  position: relative;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-left: 10px;
  /* background: yellow; */
}
.songs-play::after {
  position: absolute;
  bottom: 0;
  content: "";
  width: 100%;
  height: 1px;
  background: rgb(240, 240, 240);
}
.spl {
  border-left: 1px solid gainsboro;
  /* height: 80%; */
  box-sizing: border-box;
  padding-left: 5px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  width: 0;
  flex: 1 1 auto;
  /* background: red; */
}
.spname {
  font-size: 17px;
  /* background: red; */
}
.spinfo {
  font-size: 12px;
  color: #888;
  margin-top: 5px;
  /* background: blue; */
}
.sptext {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  word-wrap: normal;
  display: inline-block;
}
.spr {
  width: 60px;
  height: 60px;
  /* position: relative;
  right: 0; */
  /* background: chartreuse; */
  display: flex;
  align-items: center;
  justify-content: center;
}
.spr-img {
  /* width: 60%; */
  /* height: 50%; */
  display: inline-block;
  width: 22px;
  height: 22px;
  background: url(../../assets/Icould/index_icon.png) no-repeat;
  background-size: 166px 97px;
  background-position: -24px 0;
}
</style>