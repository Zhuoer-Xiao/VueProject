<template>
    <form @submit.prevent="demo">
        金额：<input type="number" v-model="userInfo.cost" placeholder="请输入金额">
        收支类型：
        支出<input type="radio" name="type" v-model="userInfo.type" value="支出" >
        收入<input type="radio" name="type" v-model="userInfo.type" value="收入"> 
        可选标签：
        <select v-model="userInfo.kind">
            <option value="0">请选择消费类别</option>
            <option value="工资收入">工资收入</option>
            <option value="饮食">饮食</option>
            <option value="穿搭">穿搭</option>
            <option value="电子产品">电子产品</option>
            <option value="游戏">游戏</option>
        </select>
        <br/><br/>
        <br/>
        <textarea v-model.lazy="userInfo.other" placeholder="备注"></textarea> 
        <br>
        <button>提交</button>
    </form>
</template>

<script>
const axios = require("axios");
export default {
    data(){
        return{
            userInfo:{
                kind:'0',
                cost:0,
                type:'支出',
                other:'',
            }
        }
    },
    methods:{
            // this.$bus.$emit('addItem',this.userInfo)
        demo(){
            if(this.userInfo.kind==0){
                alert('类型未选择')
                return
            }
            if(this.userInfo.cost<=0){
                alert('金额违法')
                return
            }
            console.log("添加功能被调用");
            console.log(JSON.stringify(this.userInfo));
            axios.post("https://qc4kzp.fn.thelarkcloud.com/addItem", this.userInfo).then(
                (response) => {
                alert("返回成功，id值为" + response.data._id);
                 this.$bus.$emit("initItem");
                 this.$bus.$emit("tableInit1");
                 this.$bus.$emit("tableInit2");
                },
                (error) => {
                alert("请求失败了", error.message);
                }
      );
      this.userInfo.cost=0
      this.userInfo.kind=''
      this.userInfo.other=''
      this.$bus.$emit('initItem')

    }
    }
}
</script>

<style scoped>
textarea{
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
}
button {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
}
</style>