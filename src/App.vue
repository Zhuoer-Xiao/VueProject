<template>
  <div id="app">
    <myHeader id="myHeader" />
    <hisInfo id="hisInfo" :items="items" />
    <restMoney id="restMoney" />
    <myFooter id="myFooter" />
    <myFuns id="myFuns" :items="items" />
  </div>
</template>

<script>
import myHeader from "@/components/myHeader";
import hisInfo from "@/components/hisInfo";
import restMoney from "@/components/restMoney";
import myFooter from "@/components/myFooter";
import myFuns from "@/components/myFuns";
const axios = require("axios");

export default {

  name: "App",
  data() {
    return {
      items: [],
    };
  },
  components: {
    myHeader,
    hisInfo,
    restMoney,
    myFooter,
    myFuns,
  },
  methods: {
    // deleteItem(_id) {
    //   console.log("删除功能被调用");
    //   axios.post("https://qc4kzp.fn.thelarkcloud.com/deleteInfo", _id).then(
    //     (response) => {
    //       alert("删除成功，id值为" + response.data._id);
    //     },
    //     (error) => {
    //       alert("请求失败了", error.message);
    //     }
    //   );
    // },
    // addItem(obj) {
    //   console.log("添加功能被调用");
    //   console.log(JSON.stringify(obj));
    //   axios.post("https://qc4kzp.fn.thelarkcloud.com/upDate", obj).then(
    //     (response) => {
    //       alert("返回成功，id值为" + response.data._id);
    //     },
    //     (error) => {
    //       alert("请求失败了", error.message);
    //     }
    //   );
    // },
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
  },
  mounted() {
    this.initItems
    this.$bus.$on("deleteItem", this.deleteItem);
    this.$bus.$on("addItem", this.addItem);
    this.$bus.$on("initItem", this.initItems);
  },
};  
</script>

<style>
#hisInfo {
  width: 40%;
  height: 50%;
  position: absolute;
}
#restMoney {
  width: 40%;
  height: 50%;
  top: 460px;
  position: absolute;
}
#myFooter {
  width: 100%;
  height: 100px;
  position: absolute;
  bottom: 0px;
}
#myFuns {
  width: 60%;
  height: 820px;
  float: right;
}
#myHeader {
  height: 10%;
}
</style>
