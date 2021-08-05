<template>
  <div>
      <div id="hisInfo">
          <hisInfo/>
      </div>
      <div id="restMoney">
          <restMoney/>
      </div>
      <div>
          <piechart/>
      </div>
  </div>
</template>

<script>
import hisInfo from '@/components/hisInfo'
import restMoney from '@/components/restMoney'
import piechart from '@/components/piechart'
export default {
    components:{
        hisInfo,restMoney,piechart
    }
}
</script>

<style>
#restMoney{
margin-left: 600px;
padding-left: 20px;

}
#hisInfo{
    margin-top: 10px;
}
</style>