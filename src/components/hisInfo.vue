<template>
    <div id="myHis" ref="chart">hisInfo模块</div>
</template>

<script>
const axios = require("axios");
let Echarts = require('echarts/lib/echarts'); //基础实例 注意不要使用import
require('echarts/lib/chart/bar'); //按需引入 bar = 柱状图
export default {
    data() { return { chart: null,mydata:[] } }, //图表实例
    mounted() {
         this.init()
        //  this.getDate()
         this.$bus.$on("tableInit1", this.init);
     },
    methods: {
        // getDate(){
        //     axios.post("https://qc4kzp.fn.thelarkcloud.com/returnInfo", {}).then(
        //         (response) => {
        //         console.log("获取初始化数据成功", response.data.result);
        //         this.mydata = JSON.parse(response.data.result);
        //         },
        //         (error) => {
        //         alert("请求失败了", error.message);
        //         }
        //     );
        // },
        init() {
            var datas=[]
            axios.post("https://qc4kzp.fn.thelarkcloud.com/tableInfo", {}).then(
                (response) => {
                console.log("获取图表初始化数据成功", response.data.result);
                datas = response.data.result;
                console.log(datas)
                this.chart = Echarts.init(this.$refs.chart);
            //3.配置数据
                let option = {
                    title:{
                        text:"近七日支出"
                    },
                    xAxis: { type: 'category', data: ['六天前', '五天前', '四天前', '三天前', '二天前', '一天前', '今天'] }, //X轴
                    yAxis: { type: 'value' }, //Y轴
                    series: [{
                        name: '支出',
                        type: 'line',
                        data: datas,
                        label: {
                            show: true,
                            position: 'right'
                    }
                    }]
            };
            // 4.传入数据
            this.chart.setOption(option);
                },
                (error) => {
                alert("请求失败了", error.message);
                }
            );
            // this.$bus.$emit('initShow')
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
        }
    }
};
</script>

<style scoped>
    div{
        /* background-color: rgb(103, 163, 241); */
        width: 600px;
        height: 400px;
        position: absolute;
    }
</style>