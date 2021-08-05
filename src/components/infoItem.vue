<template>
  <div id="all">
    <div id="container1" v-show="editFlag">
      <div id="costShow" class="littleshow">{{ item.cost }}</div>
      <div id="kindShow" class="littleshow">{{ item.kind }}</div>
      <div id="typeShow" class="littleshow">{{ item.type }}</div>
      <div id="otherShow" class="littleshow">{{ item.other }}</div>
      <div id="dateShow" class="littleshow">
        {{ item.updatedAt.slice(0, 10) }}
      </div>
      <button id="changeBtn" class="litteshow" @click="editer">修改</button>
      <button id="deleteBtn" class="litteshow" @click="handleDelete(item._id)">
        删除
      </button>
    </div>
    <div id="container2" v-show="!editFlag">
      <form @submit.prevent="updateItem">
        花费：<input
          type="number"
          v-model="item.cost"
          placeholder="请输入金额"
        />
        收支类型： 支出<input
          type="radio"
          name="type"
          v-model="item.type"
          value="支出"
        />
        收入<input type="radio" name="type" v-model="item.type" value="收入" />
        收支：<select v-model="item.kind">
          <option value="0">请选择消费类别</option>
          <option value="工资收入">工资收入</option>
          <option value="饮食">饮食</option>
          <option value="穿搭">穿搭</option>
          <option value="电子产品">电子产品</option>
          <option value="游戏">游戏</option>
        </select>
        备注：<textarea v-model.lazy="item.other" placeholder="备注"></textarea>
        <input  id="indate" type="date" v-model="item.updatedAt" />
        <button id="okBtn">完成</button>
      </form>
    </div>
  </div>
</template>

<script>
const axios = require("axios");
export default {
  data() {
    return {
      editFlag: true,
    };
  },
  props: ["item"],
  methods: {
    updateItem() {
      this.editFlag = !this.editFlag;
      var currentTime = new Date();
      var customTime = this.item.updatedAt.replace("-", "/"); //替换字符，变成标准格式
      customTime = new Date(Date.parse(customTime));

      if (currentTime < customTime) {
        alert("警告，要修改时间晚于当前时间");
      }

      alert("修改功能被调用");
      console.log(this.item);
      axios.post("https://qc4kzp.fn.thelarkcloud.com/upDate", this.item);
      alert("重新初始化");
      this.$bus.$emit("tableInit1");
      this.$bus.$emit("tableInit2");
    },
    editer() {
      this.editFlag = !this.editFlag;
    },
    handleDelete(id) {
      if (confirm("确定删除吗？")) {
        const info = { _id: id };
        console.log("删除功能被调用");
        console.log(JSON.stringify(info));
        axios.post("https://qc4kzp.fn.thelarkcloud.com/deleteInfo", info);
        alert("重新初始化");
        this.$bus.$emit("initItem");
        this.$bus.$emit("initItem");
        this.$bus.$emit("tableInit1");
        this.$bus.$emit("tableInit2");
      }
    },
  },
};
</script>

<style scoped>
#container1 {
  display: flex;
  border-style: solid;
  border-width: 1px;
}
button {
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
  margin-top: 7px;
}
.littleshow,
#container2 {
  background-color: white;
  font-size: 16px;
  text-align: center;
  line-height: 50px;
  flex-shrink: 1;
  flex-grow: 1;
  padding-left: 0;
}
#deleteBtn {
  margin-left: 2px;
  background-color: rgb(199, 11, 11);
  color: aliceblue;
}
#changeBtn {
  background-color: rgb(106, 172, 248);
  color: aliceblue;
}
#okBtn {
  background-color: rgb(89, 204, 123);
  color: aliceblue;
}
#costShow {
  width: 10%;
}
#dateShow {
  width: 20%;
}
#typeShow {
  width: 10%;
}
#kindShow {
  width: 15%;
}
#otherShow {
  width: 20%;
  text-align: left;
}
#indate{
  margin-left: 5px;
}
</style>
