<template>
  <div id="app">
    <div class="title-bar">
      <h3 class="title">全部</h3>
      <ul is="ul">
        <li
          v-for="(item, index) in singerType"
          :key="index"
        >
          {{ item }}
        </li>
      </ul>
    </div>
    <main>
      <div
        class="singer-card"
        v-for="(item, index) in musics"
        :key="index"
      >
          <span>{{item.name}}</span>
          <div class="thumbnail">
            <img
              :src="item.thumbnail"
              alt=""
            />
          </div>
          <span>{{ item.singer }}</span>
        <button @click="moveBtn(item.url)" class="play-btn">
          <img
            src="../assets/image/yinpinbofang.png"
            alt=""
          />
        </button>
      </div>
       <audio src="url" ref="audio"></audio>
    </main>
  </div>
</template>

<script>
export default {
  name: "singer",
  click: "0",
  data() {
    return {
      singerType: ["华语男", "华语女", "日韩男", "日韩女", "欧美男", "欧美女"],
      musics: [],
      url: ''
    };
  },
  components: {},
  created() {
    this.getMusic()
  },
  mounted() {},
  methods: {
    getMusic(){
         this.axios({
					method: 'get',
          url: "http://localhost:8082/music",
				}).then(res => {
           this.musics = res.data.data
				})
    },
    moveBtn(url) {
      let audio = this.$refs.audio
      audio.src = url
      audio.play()
      // audio.url = url
      // audio.play()

    }
  },
  computed: {}
};
</script>

<style scoped lang="scss">
main {
  display: flex;
  flex-wrap: wrap;
  width: 80%;
  margin: 0 auto;
}
.singer-card {
  flex: 0 0 20%;
  margin: 30px 20px;
  text-align: center;
  min-height: 350px;
  line-height: 3rem;
  position: relative;
}
.singer-card:hover button {
  display: block;
  cursor: pointer;
}

.singer-card span {
  font-size: 1.4rem;
}

.thumbnail img {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  margin-top: 40px;
  animation: moveImg 5s infinite ease;
}

@keyframes moveImg {
  to {
    transform: rotate(369deg);
  }
}

.title {
  margin-left: 13%;
}
.title-bar {
  display: flex;
  justify-content: flex-start;
  margin-top: 90px;
}
.title-bar ul {
  display: flex;
  justify-content: space-around;
  width: 600px;

  margin: 0 30px;
}
.title-bar ul li {
  height: 90px;
  line-height: 90px;
  font-size: 1.4rem;
  list-style: none;
}

a {
  text-decoration: none;
  color: black;
}
button {
  width: 100px;
  height: 50px;
  position: absolute;
  margin: auto;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: none;
  border: none;
  display: none;
}

button img {
  width: 50px;
  height: 50px;
}

.play-btn {
  outline: none;
}
</style>
