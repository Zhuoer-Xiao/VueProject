<template>
  <div id="myFuns">
    <addInfo id="addInfo" />
    <showInfo id="showInfo" :items="items">showInfo</showInfo>
  </div>
</template>

<script>
import addInfo from "@/components/addInfo";
import showInfo from "@/components/showInfo";

export default {
  components: {
    addInfo,
    showInfo,
  },
  props: ["items"],
};
</script>

<style scoped>
#addInfo {
  height: 20%;
  width: 100%;
}
#showInfo {
  height: 800px;
  width: 100%;
}
</style>
