<template>
  <div id="app">
    <logIn v-show="funs == 0"></logIn>
    <abar id="abar" :funs="funs" v-show="funs != 0" />
    <mychart v-show="funs == 1" />
    <myFuns id="myFuns" :items="items" v-show="funs == 2" />
    <userInfo id="userInfo" :myInfo="myInfo" v-show="funs == 3" />
  </div>
</template>

<script>
import abar from "@/components/abar";
import myFuns from "@/components/myFuns";
import mychart from "@/components/mychart";
import userInfo from "@/components/userInfo";
import logIn from "@/components/logIn";
const axios = require("axios");

export default {
  name: "App",
  data() {
    return {
      functions: true,
      items: [],
      funs: 0,
      myInfo: {
        username: "admin",
        vip: 2,
        userno: 12345678,
        userphone: 654321987,
      },
    };
  },
  components: {
    myFuns,
    abar,
    mychart,
    userInfo,
    logIn,
  },
  methods: {
    initItems() {
      axios.post("https://qc4kzp.fn.thelarkcloud.com/returnInfo", {}).then(
        (response) => {
          console.log("获取初始化数据成功", response.data.result);
          this.items = JSON.parse(response.data.result);
        },
        (error) => {
          alert("请求失败了", error.message);
        }
      );
    },
    changeFuns(t) {
      this.funs = t;
    },
  },
  mounted() {
    this.initItems;
    this.$bus.$on("deleteItem", this.deleteItem);
    this.$bus.$on("addItem", this.addItem);
    this.$bus.$on("initItem", this.initItems);
    this.$bus.$on("changeFuns", this.changeFuns);
  },
};
</script>

<style>
* {
  padding: 0px;
  margin: 0px;
  overflow: hidden;
}
#abar {
  z-index: 1;
  width: 100%;
  height: 50px;
}
</style>
