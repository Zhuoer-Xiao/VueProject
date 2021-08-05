<template>
<div>
    <div id="myPie" ref="chart3"></div>
</div>

</template>

<script>
const axios = require("axios");
let Echarts = require("echarts/lib/echarts"); 
require("echarts/lib/chart/pie"); 
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
      axios.post("https://qc4kzp.fn.thelarkcloud.com/piechart", {}).then(
        (response) => {
          console.log("获取图表初始化数据成功", response.data.result);
          datas = response.data.result;
          console.log(datas);
          this.chart = Echarts.init(this.$refs.chart3);
          let option = {
            title: {
              text: "本月消费结构",
            },
            series: [
              {
                name: "支出",
                type: "pie",
                data: [
                {value:datas[0], name:'穿搭'},
                {value:datas[1], name:'饮食'},
                {value:datas[2], name:'电子产品'},
                {value:datas[3], name:'游戏'}
                ],
                labelLine: {    
                    normal: {
                        length: 25,
                        length2:50
                    }
                },
              label: {
                show: true
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
        width: 600px;
        height: 400px;
        padding-left: 10px;
}
</style>