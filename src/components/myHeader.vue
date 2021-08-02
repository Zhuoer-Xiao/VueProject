<template>
      <header>
        <div id="head1">
            <div class="myhead">在线记账系统

            </div>
        </div>
    </header>
</template>

<script>
export default {
    methods:{
        function1(){
            alert("执行功能1")
        },
        function2(){
            alert("执行功能2")
        },
        function3(){
            alert("执行功能3")
        },
        function4(){
            alert("执行功能4")
        }
    }
}
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
    list-style: none;
}

#head1{
    width:100%;
}

.myhead{
    width: 100%;
    height: 10%;
}

.funItem{
    background-color: white;
    font-size: 30px;
    text-align: center;
    line-height: 50px;
    flex-shrink: 1;
    flex-grow: 1;
}

#name{
    width: 50%;
    text-align: left;
}
.funItem:nth-child(2):hover{
    background-color: rgb(100, 166, 241);
}

.funItem:nth-child(3):hover{
    background-color: rgb(100, 166, 241);
}

.funItem:nth-child(4):hover{
    background-color: rgb(100, 166, 241);
}

.funItem:nth-child(5):hover{
    background-color: rgb(100, 166, 241);
}

.funItem:nth-child(6):hover{
    background-color: rgb(100, 166, 241);
}
</style>