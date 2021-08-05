<template>
  <div>
    <div id="mypage">
      <ul>
        <li>
          <div>username:&nbsp;&nbsp;{{ myInfo.username }}</div>
        </li>
        <li>
          <div>会员等级：&nbsp;&nbsp;{{ myInfo.vip }}</div>
        </li>
        <li>
          <div>我的账号：{{ myInfo.userno }}</div>
        </li>
        <li>
          <div>我的绑定电话：{{ myInfo.userphone }}</div>
        </li>
      </ul>
      <button @click="userQuit">注销</button>
      <!-- <br />
      <br />
      <br />
      <br />
      <br />
      <br />
      <br />
      <br />
      <button id="showit" @click="yes">更新日志</button>
      <div v-show="seeit">
        <h2>
          8月4日更新
        </h2>
        <p>
          &nbsp;&nbsp;优化了系统界面<br />
          &nbsp;&nbsp;增加了个人信息页面<br />
          &nbsp;&nbsp;优化了修改日期的功能，修改日期超出当前日期会给予警告
        </p>
      </div> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      seeit: false,
    };
  },
  props: ["myInfo"],
  methods: {
    userQuit() {
      this.$bus.$emit("changeFuns", 0);
    },
    yes() {
      this.seeit = !this.seeit;
    },
  },
};
</script>

<style scoped>
#mypage {
  width: 60%;
  height: 1700px;
  /* background-color: rgb(245, 238, 238); */
  margin: 0px auto;
  box-shadow: 2px 2px 10px black;
}
li {
  margin-left: 150px;
  margin-bottom: 5px;
  font-size: 24px;
}
div {
  color: grey;
}
button {
  margin-top: 20px;
  margin-left: 150px;
  height: 30px;
  position: flex;
  padding: 4px 12px;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
  background-color: rgb(199, 11, 11);
  color: aliceblue;
}
#showit {
  background-color: grey;
}
</style>
