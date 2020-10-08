<template>
  <div class="hotmusic-main">
    <div class="hotmusic">
      <!-- 上部图片 -->
      <div class="hottop">
        <div class="hotcontent">
          <div class="hotpic"></div>
        </div>
      </div>
      <!-- 音乐列表 -->
      <div class="hotlist">
        <div class="hotlist-ul">
          <a
            href="javascript:;"
            class="hotlist-li"
            v-for="(item,index) in hotmusicsinfo"
            :key="index"
            @click="transmithminfo(index)"
          >
            <div
              class="hotlist-num"
              :class="{top3:index<3}"
              v-text="index<9?'0'+(index+1):(index+1)"
            ></div>
            <div class="hotlist-play">
              <div class="hpl">
                <div class="hptext spname">{{item.hmname}}</div>
                <div class="hptext spinfo">{{item.hmsonger}} -- {{item.hmalbum}}</div>
              </div>
              <div class="hpr">
                <span class="hpr-img"></span>
              </div>
            </div>
          </a>
        </div>
      </div>
      <!-- 下载网易云 -->
      <div class="downloadapp">
        <a href="https://m.music.163.com/m/applink/?scheme=orpheus%3A%2F%2Fplaylist%2F3778678" class="godownload">查看完整榜单</a>
      </div>
    </div>
  </div>
</template>

<script>
import transmithotmusicinfo from "../../assets/transmithminfo";

export default {
  data() {
    return {
      //最新音乐 音乐信息
      hotmusicsinfo: [],
    };
  },
  methods: {
    showhotsongs(index) {
      axios.get("https://autumnfish.cn/toplist").then((response) => {
        //热歌榜id
        let hmlistid = response.data.list[3].id;
        for (let i = 0; i < 20; i++) {
          const data = {};

          axios
            .get("https://autumnfish.cn/playlist/detail?id=" + hmlistid)
            .then((response) => {
              //热歌id
              data.hotmusicid = response.data.privileges[i].id;
              //热歌url
              axios
                .get("https://autumnfish.cn/song/url?id=" + data.hotmusicid)
                .then((response) => {
                  data.hmurl = response.data.data[0].url;
                });
              // 这里时第一个axios的返回，下面开始调另一个axios
              axios
                .get("https://autumnfish.cn/song/detail?ids=" + data.hotmusicid)
                .then((response) => {
                  // console.log(response)
                  //填入歌名
                  data.hmname = response.data.songs[0].name;
                  //填入歌手
                  data.hmsonger = response.data.songs[0].ar[0].name;
                  //填入专辑
                  data.hmalbum = response.data.songs[0].al.name;
                  //填入歌曲图片
                  data.hmimg = response.data.songs[0].al.picUrl;
                  this.hotmusicsinfo.push(data);
                });
              // 这里的代码会与上面的axios同时执行
            });
        }
      });
      // console.log(this.hotmusicsinfo);
    },
    transmithminfo(index) {
      transmithotmusicinfo.$emit(
        "transmithotmusicinfo",
        this.hotmusicsinfo,
        index
      );
    },
  },
  created() {
    this.showhotsongs();
  },
};
</script>

<style scoped>
.hotmusic-main {
  width: 100vw;
  position: relative;
  top: calc(10vh + 40px);
  overflow-x: hidden;
  overflow-y: scroll;
}
.hottop {
  position: relative;
  padding-top: 38.9%;
  overflow: hidden;
  background: url(../../assets/Icould/bghot.jpg);
  background-size: contain;
}
.hottop::after {
  content: " ";
  position: absolute;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
  background-color: rgba(128, 67, 67, 0.2);
}
.hotcontent {
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: 2;
  padding-left: 20px;
  box-sizing: border-box;
}
.hotpic {
  width: 142px;
  height: 67px;
  background: url(../../assets/Icould/index_icon.png);
  background-position: -24px -30px;
  background-size: 166px 97px;
}

.hotlist-ul {
  position: relative;
}
.hotlist-li {
  color: #333;
  display: flex;
  justify-content: center;
  position: relative;
}
.hotlist-num {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  font-size: 17px;
}
.top3 {
  color: #df3436;
}
.hotlist-play {
  position: relative;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.hotlist-play::after {
  position: absolute;
  bottom: 0;
  content: "";
  width: 100%;
  height: 1px;
  background: rgb(240, 240, 240);
}
.hpl {
  border-left: 1px solid gainsboro;
  box-sizing: border-box;
  padding-left: 8px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  width: 0;
  flex: 1 1 auto;
}
.spname {
  font-size: 17px;
}
.spinfo {
  font-size: 12px;
  color: #888;
  margin-top: 5px;
}
.hptext {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  word-wrap: normal;
  display: inline-block;
}
.hpr {
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.hpr-img {
  display: inline-block;
  width: 22px;
  height: 22px;
  background: url(../../assets/Icould/index_icon.png) no-repeat;
  background-size: 166px 97px;
  background-position: -24px 0;
}
.downloadapp {
  height: 55px;
  line-height: 55px;
  text-align: center;
  margin-bottom: 10vh;
}
.godownload {
  display: inline-block;
  color: #999;
  padding-right: 14px;
  background: url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNCAyMiI+PHBhdGggZmlsbD0ibm9uZSIgc3Ryb2tlPSIjY2NjIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgZD0iTTEgMWwxMCAxMEwxIDIxIi8+PC9zdmc+)
    100% no-repeat;
  background-size: 7px 12px;
}
.sjs {
  width: 100vw;
  height: 150vh;
  background: linear-gradient(to bottom, blue, red);
}
</style>