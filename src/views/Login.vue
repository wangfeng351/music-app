<template>
  <div class="login">
    <div class="viewport">
      <input
        type="radio"
        name="slider"
        id="pic1"
        checked
      >
      <input
        type="radio"
        name="slider"
        id="pic2"
        checked
      >
      <input
        type="radio"
        name="slider"
        id="pic3"
        checked
      >
      <input
        type="radio"
        name="slider"
        id="pic4"
        checked
      >
      <input
        type="radio"
        name="slider"
        id="pic5"
        checked
      >

    </div>
    <div class="wrap">
      <img
        src="../assets/image/1.jpg"
        alt=""
      >
      <img
        src="../assets/image/2.jpg"
        alt=""
      >
      <img
        src="../assets/image/3.jpg"
        alt=""
      >
      <img
        src="../assets/image/4.jpg"
        alt=""
      >
      <img
        src="../assets/image/5.jpg"
        alt=""
      >
      <img
        src="../assets/image/1.jpg"
        alt=""
      >
    </div>
    <div class="page">
      <label for="pic1"></label>
      <label for="pic2"></label>
      <label for="pic3"></label>
      <label for="pic4"></label>
      <label for="pic5"></label>
    </div>
    <!-- 登录的窗口 -->
    <div class="login-content">
      <div class="tab">
        <input
          type="radio"
          id="testTabOne"
          class="test-radio"
          name="tab"
          checked="checked"
        />
        <label
          class="testTabLabel loginLabel"
          for="testTabOne"
           @click="account='', password=''"
        >登录</label>
        <div class="testTabCon">
          <div class="contentDiv">
            <div class="login-left">
                <table>
                  <tr>
                    <td>账号:</td>
                    <td><input type="text" v-model="account"></td>
                  </tr>
                  <tr>
                    <td>密码:</td>
                    <td><input type="password" v-model="password"></td>
                  </tr>
                  <tr>
                    <td colspan="2">
                      <button class="login-btn" @click="signIn()">登录</button>
                    </td>
                  </tr>
                </table>
            </div>
            <div class="login-right"><img
                src="https://cdn.colorhub.me/M1H4PLrOSsyS8swZzpVf3w4KlNMom-NTkS9K1TkWCQo/auto/280/0/ce/0/bG9jYWw6Ly8vOWEv/MjIvZDI3OGZlZGU0/YTNjNjczODBiZTJm/Mjg1ZDZhYjE4OTQ0/MTA4OWEyMi5qcGc.jpg"
                alt=""
              >
            </div>
          </div>
        </div>
      </div>
      <div class="tab">
        <input
          type="radio"
          id="testTabTwo"
          class="test-radio"
          name="tab"
        />
        <label
          class="testTabLabel"
          for="testTabTwo"
          @click="account='', password=''"
        >注册</label>
        <div class="testTabCon">
          <div class="contentDiv">
            <div class="register-left"><img
                src="https://i0.hippopx.com/photos/179/138/424/people-woman-earphone-earrings-preview.jpg"
                alt=""
              ></div>
            <div class="register-right">
                <table>
                  <tr>
                    <td>账号:</td>
                    <td><input type="text" v-model="account"></td>
                  </tr>
                  <tr>
                    <td>密码:</td>
                    <td><input type="text" v-model="password"></td>
                  </tr>
                  <tr>
                    <td colspan="2">
                      <button class="login-btn" @click="signUp()">注册</button>
                    </td>
                  </tr>
                </table>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      click: 0,
      password: '',
      account: ''
    };
  },

  components: {},
  created() {},
  mounted() {},
  methods: {
    signIn(){
      let pattern = /^([A-Za-z0-9_\-\.])+\@(163.com|qq.com|42du.cn)$/;
      let phonePattern = /^[1](([3][0-9])|([4][5-9])|([5][0-3,5-9])|([6][5,6])|([7][0-8])|([8][0-9])|([9][1,8,9]))[0-9]{8}$/
      let phone = ''
      let email = ''
      let flag = false
      if(pattern.test(this.account)){
        email = this.account
        flag = true
      }else if(phonePattern.test(this.account)){
        phone = this.account
        flag = true
      }else {
        alert("账号格式不正确")
      }
      this.axios({
					method: 'post',
          url: "http://localhost:8082/user/signIn",
          data: {
            email: email ,
            phoneNumber: phone,
            password: this.password
          }
				}).then(res => {
           console.log(res.data.code)
           if(res.data.code == 1){
             localStorage.setItem('user', JSON.stringify(res.data.data))
                  this.$router.push({
                    path: '/nav'
                  })
           }else {
             alert("账号密码不正确")
           }
				})
    },

    signUp(){
      let pattern = /^([A-Za-z0-9_\-\.])+\@(163.com|qq.com|42du.cn)$/;
      let phonePattern = /^[1](([3][0-9])|([4][5-9])|([5][0-3,5-9])|([6][5,6])|([7][0-8])|([8][0-9])|([9][1,8,9]))[0-9]{8}$/
      let phone = ''
      let email = ''
      let flag = false
      if(pattern.test(this.account)){
        email = this.account
        flag = true
      }else if(phonePattern.test(this.account)){
        phone = this.account
        flag = true
      }else {
        alert("账号格式不正确")
      }
      if(flag){
        this.axios({
					method: 'post',
          url: "http://localhost:8082/user/signUp",
          data: {
            email: email ,
            phoneNumber: phone,
            password: this.password
          }
				}).then(res => {
           if(res.data.data == "注册成功"){
              this.account = ''
              this.password = ''
              alert(res.data.data)
           }else {
             alert(res.data.data)
           }
				})
      }

    }
  },
  computed: {}
};
</script>

<style scoped lang="scss" >
.viewport {
  overflow: hidden;
  margin-left: 0;
}
.wrap {
  position: relative;
  width: 600vw;
  overflow: hidden;
  // animation: carousel linear 10s infinite 0s normal;
}
.wrap img {
  width: 100vw;
  height: auto;
  float: left;
}
@keyframes carousel {
  0% {
    left: 0;
  }
  30% {
    left: -0vw;
  }
  40% {
    left: -100vw;
  }
  50% {
    left: -100vw;
  }
  60% {
    left: -200vw;
  }
  70% {
    left: -200vw;
  }
  80% {
    left: -300vw;
  }
  90% {
    left: -300vw;
  }
  100% {
    left: -400vw;
  }
}
.login-content {
  position: fixed;
  width: 50%;
  height: 600px;
  margin: auto;
  z-index: 666;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
  margin-top: 10%;
}
input {
  display: none;
}
.contentDiv {
  width: 100%;
  height: 100%;
  display: flex;
}
.login-left {
  width: 450px;
  height: 100%;
  text-align: center;
}
.login-right {
  width: 350px;
}
.login-right img {
  width: 100%;
  height: 100%;
}

table {
  margin: 50px auto;

  tr {
    height: 40px;
    line-height: 40px;

    text-align: center;
  }

  td {
    height: 70px;
    line-height: 40px;

    color: gray;
  }
}
.login-btn {
  background: rgb(36, 34, 34);
  width: 260px;
  height: 40px;
  border-radius: 5px;
  border: none;
  margin-top: 30px;
  color: gray;
  font-size: 1.4rem;
}
.login-content input {
  display: block;
  box-shadow: none;
  margin: 0px 20px;
}
.register-left {
  flex: 0 0 40%;
  img {
    width: 100%;
    height: 100%;
  }
}
.register-right {
  flex: 0 0 60%;
}

.tab {
  width: 25%;
  float: left;
  margin-right: -1px;
  box-sizing: border-box;
}
.tab .testTabLabel {
  text-align: center;
  display: block;
  height: 55px;
  margin-top: 30px;
  background: rgb(36, 34, 34);
  line-height: 55px;
  color: gray;
}

.tab .test-radio,
.tab .testTabCon {
  position: absolute;
  left: -999em;
  width: 100%;
  height: 100%;
  background: rgb(73, 73, 73);
}
.test-radio:checked ~ .testTabLabel {
  background: rgb(73, 73, 73);
  position: relative;
  z-index: 1;
  height: 55px;
}
.test-radio:checked ~ .testTabCon {
  left: 0;
  border-top: 0;
  width: 763px;
  padding: 0.5em 0.5em;
}
</style>
