<template>
  <div>
    <div id="container1" v-show="editFlag">
      <div class="littleshow">花费：{{ item.cost }}</div>
      <div class="littleshow">收支：{{ item.kind }}</div>
      <div class="littleshow">收支类型：{{ item.type }}</div>
      <div class="littleshow">备注：{{ item.other }}</div>
      <div class="littleshow">日期：{{ item.updatedAt.slice(0, 10) }}</div>
      <button class="litteshow" @click="editer">修改</button>
      <button class="litteshow" @click="handleDelete(item._id)">删除</button>
    </div>
    <div id="container2" v-show="!editFlag">
      <form @submit.prevent="updateItem">
          花费：<input type="number" v-model="item.cost" placeholder="请输入金额">
          收支类型：
        支出<input type="radio" name="type" v-model="item.type" value="支出" >
        收入<input type="radio" name="type" v-model="item.type" value="收入"> 
          收支：<select v-model="item.kind">
            <option value="0">请选择消费类别</option>
            <option value="工资收入">工资收入</option>
            <option value="饮食">饮食</option>
            <option value="穿搭">穿搭</option>
            <option value="电子产品">电子产品</option>
            <option value="游戏">游戏</option>
        </select>
         备注：<textarea v-model.lazy="item.other" placeholder="备注"></textarea> 
         <button>完成</button>
      </form>
    </div>
  </div>
</template>

<script>
const axios = require("axios");
export default {
  //声明接收todo
  data() {
    return {
      editFlag: true,
    };
  },
  props: ["item"],
  methods: {
    updateItem(){
        this.editFlag=!this.editFlag
        alert('修改功能被调用')
        console.log(this.item)
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
        // this.$bus.$emit("initItem");
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
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
}
.littleshow ,#container2{
  background-color: white;
  font-size: 10px;
  text-align: center;
  line-height: 50px;
  flex-shrink: 1;
  flex-grow: 1;
  padding-left: 0;
}
</style>
