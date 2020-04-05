<template>
  <div id="app">
    <div class="title-bar">
      <h3>全部歌单</h3>
    </div>

    <main>
      <div
        class="song-card"
        v-for="(item, index) in albums"
        :key="index"
      >
        <div class="song-img">
          <img
            :src="item.thumbnail"
            alt=""
          />
        </div>
        <div class="song-bottom">
          <p>
          <span class="song-bottom">收藏</span>
          <img
              src="../assets/image/collection.png"
              alt=""
              style="width:30px;height:30px"
           >
            </p>
          <span>{{ item.album }}</span>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "song",
  data() {
    return {
      active: true,
      albums: [],
      userMusic: [],
      user: JSON.parse(localStorage.getItem("user")),
    };
  },
  components: {},
  created() {
    this.getAlbum()
    this.getFavorite()
  },
  mounted() {},

  methods: {
     getAlbum(){
         this.axios({
					method: 'get',
          url: "http://localhost:8082/music",
				}).then(res => {
           this.albums = res.data.data
				})
    },
    getFavorite(){
      let account = ''
      if(this.user.phoneNumber != null){
        account = this.user.phoneNumber
      }else {
        account = this.user.email
      }
      this.axios({
					method: 'get',
          url: "http://localhost:8082/userMusic/user/" + 1,
				}).then(res => {
           this.userMusic = res.data.data
           console.log(this.user)
				})
    }
  },
  computed: {}
};
</script>

<style scoped lang="scss">
#app {
  margin-top: 90px;
  padding-top: 20px;
}
main {
  width: 80%;
  min-height: 600px;
  display: flex;
  flex-wrap: wrap;
  margin: 0 auto;
}
h3 {
  margin-left: -90%;
}
.song-card {
  width: 306px;
  height: 300px;

  flex: 0 0 18%;
  margin: 30px 10px;
}
.song-card span {
  font-size: 1.3rem;
}
.song-card img {
  width: 100%;
  height: 100%;
}

.title-bar {
  margin-left: 10%;
}
.song-bottom {
  width: 100%;
  height: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  p {
    display: flex;
    height: auto;
  }
  span {
    margin-left: 2px;
    width: 100%;
  }
}
</style>
