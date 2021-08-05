<template>
  <div id="mybar">
    <ul>
      <li @click="function4" id="myTitle">
        欢迎使用在线记账系统
      </li>
      <li class="funs" @click="function1">
        明细
      </li>
      <li class="funs" @click="function2">
        图表
      </li>
      <li class="funs" @click="function3">
        我的账号
      </li>
    </ul>
  </div>
</template>

<script>
export default {
    props:['funs'],
    methods:{
        function1(){
            alert("查看明细")
            this.$bus.$emit('initItem')
            this.$bus.$emit("changeFuns",2)
        },
        function2(){
            alert("查看图表")
        this.$bus.$emit("changeFuns",1)
        },
        function3(){
            alert("我的信息")
            this.$bus.$emit("changeFuns",3)
        },
        function4(){
            alert("此系统尚在优化中   ——xze")
        }
    }
    
};
</script>

<style scoped>
#mybar {
  width: 100%;
  height: 50px;
  background-color: rgb(70, 150, 241);
}
li {
  float: left;
  list-style: none;
  height: 50px;
  background-color: rgb(70, 150, 241);
  width: 20%;
  line-height: 50px;
  text-align: center;
  color: #fff;
}
#myTitle {
  width: 40%;
  font-size: 20px;
  color: black;
  background-color: rgb(70, 150, 241);
}
.funs:hover {
  background-color: rgb(63, 175, 240);
}
ul{
    width: 100%;
}
#myTitle:hover{
  background-color: rgb(63, 175, 240);
}
</style>
