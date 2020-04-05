<template>
  <div>
    <div id="nav">
      <div class="nav-left">
        <ul class="left-ul">
          <li>
            <img
              src="../assets/image/yinle.png"
              alt
            />
          </li>
          <li class="active">推荐</li>
          <li>排行榜</li>
          <li>
            <router-link to="home">歌手</router-link>
          </li>
          <li>
            <router-link to="about">歌单</router-link>
          </li>
        </ul>
      </div>
      <div class="nav-right">
        <div
          style="display:flex"
          v-if="avatar === '' "
        >
          <li>
            <router-link to="/login">登录</router-link>
          </li>
          <li>/</li>
          <li>注册</li>
        </div>
        <div
          style="display:flex;"
          v-if="avatar !== '' "
        >
          <el-avatar
            :size="60"
            src="https://empty"
          >
            <img :src="avatar" />
          </el-avatar>
          <el-button
            @click="exist()"
            style="margin-left:5px"
            type="info"
          >注销</el-button>
        </div>
      </div>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: JSON.parse(localStorage.getItem("user")),
      avatar: ""
    };
  },

  components: {},
  created() {
    if (this.user != null) {
      this.avatar = this.user.avatar;
    }
  },
  mounted() {},
  methods: {
    exist() {
      localStorage.removeItem("user");
      this.avatar = "";
    }
  },
  computed: {}
};
</script>



<style lang="scss">
#app {
  width: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  font-size: 1.6rem;
  background: rgb(153, 153, 153);
}

#nav {
  width: 100%;
  display: flex;
  justify-content: space-between;
  border-bottom: 2px dotted #eeeeee;
  position: fixed;
  z-index: 22;
  background: rgb(40, 40, 40);
  color: #ffffff;
  height: 90px;
  top: 0;
  left: 0;

  a {
    font-weight: bold;
    color: #ffffff;
    text-decoration: none;

    &.router-link-exact-active {
      color: rgb(153, 153, 153);
      border-bottom: 6px solid #ffffff;
      display: block;
    }
  }
}
.left-ul {
  display: flex;
  justify-content: flex-start;

  margin: auto;
  margin-left: -90px;
}
.left-ul li {
  margin-left: 10px;
  width: 100px;
}
.left-ul li img {
  width: 100%;
  height: 100%;
}

.nav-right {
  display: flex;
  margin-right: 40px;
  align-items: center;
}

.nav-right li {
  height: 90px;
  line-height: 90px;
  display: block;
  margin-left: -25px;
  width: 60px;
}

ul li {
  height: 90px;
  line-height: 90px;
  display: block;
}
login-li {
  margin-left: 1px;
  background: red;
}
input {
  height: 34px;
  border-radius: 4px;
  line-height: 90px;
  border: none;
  width: 270px;

  margin-top: 28px;
  margin-right: 50px;
}

#singer {
  min-height: 500px;
}
</style>

