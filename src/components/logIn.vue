<template>
  <div id="logsys">
    <h1>
      &nbsp;&nbsp;&nbsp;&nbsp;欢迎使用在线记账系统
    </h1>
    <div id="loginfo">
      <div>
        用户名：
      </div>
      &nbsp;&nbsp;&nbsp;&nbsp;<input type="text" v-model="username" />
      <br />
      <div>
        密码：
      </div>
      &nbsp;&nbsp;&nbsp;&nbsp;<input type="password" v-model="psd" />
      <br />
      <button @click="login">login</button>
      <button @click="register">注册</button>
      <button @click="forgetpsd">忘记密码</button>
      <p>默认用户名为admin，密码为1234</p>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    login() {
      if (this.username == "admin" && this.psd == 1234) {
        alert("登录成功");
        this.$bus.$emit("changeFuns", 1);
      } else {
        alert("登陆失败");
      }
    },
    register() {
      alert("注册功能未开放");
    },
    forgetpsd() {
      alert(1234);
    },
  },
  data() {
    return {
      username: "",
      psd: null,
    };
  },
};
</script>

<style scoped>
#logsys {
  margin: 270px 550px;
  width: 35%;
  height: 230px;
  background-color: rgb(170, 228, 243);
  border-radius: 12px;
  padding: auto;
  overflow: hidden;
}
button {
  color: rgb(255, 254, 254);
  margin-left: 5px;
  margin-top: 5px;
  height: 30px;
  position: flex;
  padding: 4px 12px;
  margin-bottom: 3px;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
  background-color: rgb(39, 70, 158);
}
#loginfo {
  margin-top: 30px;
  margin-left: 200px;
}
h1 {
  margin-left: 128px;
}
</style>
