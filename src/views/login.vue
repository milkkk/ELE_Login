<template>
  <div class="login">
    <div class="logo">
      <img src="http://shadow.elemecdn.com/faas/h5/static/logo.ba876fd.png" alt />
    </div>
    <InputGroup
      type="text"
      v-model="phone"
      placeholder="手机号"
      :btnText="btnText"
      :error="error.phone"
      :disabled="disabled"
      style="margin-top:15px;"
      @btnClick="verification"
    ></InputGroup>
    <InputGroup
      type="text"
      v-model="password"
      placeholder="验证码"
      style="margin-top:15px;"
      :error="error.password"
    ></InputGroup>
    <p class="agreement">
      新用户登录即自动注册，并表示已同意
      <a
        href="https://h5.ele.me/service/agreement/#initTitle=用户服务协议&key=ruleQue18"
      >《用户服务协议》</a>
    </p>
    <div class="btn-group">
      <button @click="login">登录</button>
    </div>
    <div class="about">
      <a href="#">关于我们</a>
    </div>
  </div>
</template>
<script>
import InputGroup from "../components/InputGroup";
export default {
  name: "Login",
  data() {
    return {
      btnText: "获取验证码",
      phone: "",
      password: "",
      disabled: false,
      error: {}
    };
  },
  methods: {
    verification() {
      if (this.isPhone()) {
        //发送验证码 倒计时
        this.disabled = true;
        var time = 60;
        this.error = {};
        var timer = setInterval(() => {
          //time到0停止计时
          if (time == 0) {
            this.disabled = false;
            this.btnText = "获取验证码";
            clearInterval(timer);
            return false;
          }
          this.btnText = time + "秒后重新发送";
          time--;
        }, 1000);
      } else {
        this.error = {
          phone: "手机号码有误"
        };
      }
    },
    isPhone() {
      if (/^[1][3,4,5,7,8][0-9]{9}$/.test(this.phone)) {
        return true;
      } else {
        return false;
      }
    },
    login() {
      if (this.phone == "1" && this.password == "2") {
        localStorage.ele_isLogin = true;
        this.$router.push("/");
      }
    }
  },
  components: {
    InputGroup
  }
};
</script>
<style scoped>
.login {
  width: 100%;
  background: #fff;
  height: 100%;

  padding: 0px 15px;
  padding-top: 40px;
  box-sizing: border-box;
}
.logo {
  width: 100%;
  text-align: center;
}
.login img {
  width: 150px;
  padding: 0px 10px;
  box-sizing: border-box;
}
.agreement {
  margin-top: 15px;
  color: #aaa;
}
.agreement a {
  color: #1f8bda;
  text-decoration: none;
}
.agreement a:hover,
.agreement a:active,
.agreement a:link,
.agreement a:visited {
  color: #1f8bda;
}
.btn-group {
  width: 100%;
  height: 40px;
}
.btn-group button {
  display: block;
  width: 100%;
  height: 100%;
  text-align: center;
  background: #5bda73;
  color: #fff;
  line-height: 40px;
  margin-top: 20px;
  border-radius: 4px;
  font-size: 16px;
  text-decoration: none;
  border: none;
  outline: none;
}
.about {
  width: 100%;
  margin-top: 10px;
  text-align: center;
}
.about a {
  text-align: center;
  color: #aaa;
  font-size: 12px;
  text-decoration: none;
}
</style>