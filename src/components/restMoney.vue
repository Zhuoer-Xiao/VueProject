<template>
  <div id="myHis" ref="chart2"></div>
</template>

<script>
const axios = require("axios");
let Echarts = require("echarts/lib/echarts");
require("echarts/lib/chart/bar"); 
export default {
  data() {
    return { chart: null, mydata: [] };
  }, 
  mounted() {
    this.init();
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
                "本月收入",
                "本月支出"
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
          this.chart.setOption(option);
        },
        (error) => {
          alert("请求失败了", error.message);
        }
      );
    },
  },
};
</script>

<style scoped>
div {
  /* background-color: rgb(167, 41, 41); */
        width: 600px;
        height: 400px;
        padding-left: 10px;
}
</style>
