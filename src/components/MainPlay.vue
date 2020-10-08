<template>
  <div class="Main-Play-main">
    <div class="content">
      <div class="left">
        <div class="musicimg">
          <img class="playdefaultimg" :src="musicimg" alt />
        </div>
      </div>
      <div class="right">
        <div class="playinfo">
          <div class="musicinfo">
            <div class="musicname">{{musicname}}</div>

            <div class="songer">{{songer}}</div>
          </div>
        </div>
        <audio class="playmusic" :src="musicurl" controls autoplay loop></audio>
      </div>
    </div>
  </div>
</template>

<script>
import transmithotmusicinfo from "../assets/transmithminfo";
import transmitnewmusicinfo from "../assets/transmitnminfo";

export default {
  data() {
    return {
      musicimg:
        "https://p1.music.126.net/ma8NC_MpYqC-dK_L81FWXQ==/109951163250233892.jpg?param=50y50",
      musicname: "网易云音乐",
      songer: "做你最喜欢的音乐",
      musicurl: null,
    };
  },
  methods: {
    hotmusics() {
      transmithotmusicinfo.$on(
        "transmithotmusicinfo",
        (hotmusicsinfo, index) => {
          this.musicimg = hotmusicsinfo[index].hmimg;
          this.musicname = hotmusicsinfo[index].hmname;
          this.songer = hotmusicsinfo[index].hmsonger;
          this.musicurl = hotmusicsinfo[index].hmurl;
          // console.log(hotmusicsinfo);
        }
      );
    },

    newmusics() {
      transmitnewmusicinfo.$on(
        "transmitnewmusicinfo",
        (newsongsinfo, index) => {
          this.musicimg = newsongsinfo[index].nmimg;
          this.musicname = newsongsinfo[index].nmname;
          this.songer = newsongsinfo[index].nmsonger;
          this.musicurl = newsongsinfo[index].nmurl;
          // console.log(newsongsinfo)
        }
      );
    },

    searchtoplay(){

    }
  },
  created() {
    this.hotmusics();
    this.newmusics();
    this.searchtoplay();
  },
};
</script>

<style scoped>
.Main-Play-main {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100vw;
  height: 10vh;
  background: rgb(241, 243, 244);
  z-index: 35;
}
.Main-Play-main::before {
  content: "";
  position: absolute;
  width: 100%;
  height: 1px;
  background: rgb(220, 220, 220);
  top: 0;
  left: 0;
}
.content {
  display: flex;
  justify-content: center;
}
.left {
  width: 10vh;
  height: 10vh;
  display: flex;
  align-items: center;
  justify-content: center;
  /* background: red; */
}
.left::before {
  content: "";
  position: absolute;
  top: 1vh;
  right: calc(100vw - 10vh);
  height: 8vh;
  width: 1px;
  background: rgb(220, 220, 220);
}
.musicimg {
  width: 75%;
  height: 75%;
}
.playdefaultimg {
  width: 100%;
  height: 100%;
}
.right {
  width: calc(100vw - 10vh);
  height: 10vh;
  /* background: yellow; */
  display: flex;
  flex-direction: column;
}
.playinfo {
  width: 100%;
  height: 60%;
  font-size: 5px;
  display: flex;
  /* justify-content: center; */
  align-items: center;
  /* background: wheat; */
}
.musicinfo {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  /* word-wrap: normal; */
  /* display: inline-block; */
  display: flex;
  /* align-items: center ; */
  align-items: flex-end;
}
.musicname {
  font-size: 17px;
  color: #333;
  margin-left: 15px;
  padding-right: 10px;
  display: inline-block;
}
.songer {
  font-size: 12px;
  color: #888;
  padding-left: 3px;
  display: inline-block;
}
/* .musicimg.songer{
    vertical-align: sub;
} */
.playmusic {
  width: 100%;
  height: 35%;
  /* position: relative; */
  /* bottom: -6vh; */
}
</style>