<template>
  <div id="myHis" ref="chart2"></div>
</template>

<script>
const axios = require("axios");
let Echarts = require("echarts/lib/echarts"); //基础实例 注意不要使用import
require("echarts/lib/chart/bar"); //按需引入 bar = 柱状图
export default {
  data() {
    return { chart: null, mydata: [] };
  }, //图表实例
  mounted() {
    this.init();
    //  this.getDate()
    this.$bus.$on("tableInit2", this.init);
  },
  methods: {
    init() {
      var datas = [];
      axios.post("https://qc4kzp.fn.thelarkcloud.com/restMoneyInfo", {}).then(
        (response) => {
          console.log("获取图表初始化数据成功", response.data.result);
          datas = response.data.result;
          console.log(datas);
          this.chart = Echarts.init(this.$refs.chart2);
          //3.配置数据
          let option = {
            title: {
              text: "剩余资金",
            },
            yAxis: {
              type: "category",
              data: [
                "默认账户",
                "本月总收入",
                "本月总支出"
              ],
            }, //X轴
            xAxis: { type: "value" }, //Y轴
            series: [
              {
                name: "支出",
                type: "bar",
                data: datas,
              label: {
                show: true,
                position: 'right'
              }
              }
            ],
          };
          // 4.传入数据
          this.chart.setOption(option);
        },
        (error) => {
          alert("请求失败了", error.message);
        }
      );
      //2.初始化
      // this.chart = Echarts.init(this.$refs.chart);
      // //3.配置数据
      // let option = {
      //     title:{
      //         text:"近七日支出"
      //     },
      //     xAxis: { type: 'category', data: ['六天前', '五天前', '四天前', '三天前', '二天前', '一天前', '今天'] }, //X轴
      //     yAxis: { type: 'value' }, //Y轴
      //     series: [{
      //         name: '支出',
      //         type: 'bar',
      //         data: datas
      //     }]
      // };
      // // 4.传入数据
      // this.chart.setOption(option);
    },
  },
};
</script>

<style scoped>
div {
  /* background-color: rgb(167, 41, 41); */
  padding-top: 50px;
        width: 500px;
        height: 200px;
        position: absolute;
}
</style>
