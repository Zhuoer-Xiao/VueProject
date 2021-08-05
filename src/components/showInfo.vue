<template>
  <div>
    <ul id="mT">
      <div id="b1">花费</div>
      <div id="b2">收支</div>
      <div id="b3">收支类型</div>
      <div id="b4">备注</div>
      <div id="b5">日期</div>
    </ul>
    <ul class="itemMain">
      <infoItem
        class="infoItem"
        v-for="item in items"
        :key="item._id"
        :item="item"
      />
    </ul>
  </div>
</template>

<script>
import infoItem from "@/components/infoItem";
export default {
  mounted() {
    this.$bus.$on("initShow", this.init);
  },
  components: {
    infoItem,
  },
  methods: {
    init() {
      this.$bus.$emit("initItem");
      this.$bus.$emit("tableInit");
    },
  },
  props: ["items"],
};
</script>

<style scoped>
.itemMain {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 10px;
  height: 720px;
  overflow: scroll;
}
.infoItem {
  width: 100%;
  position: relative;
  height: 40px;
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
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}
#mT {
  display: flex;
  text-align: center;
}
#b1 {
  width: 15%;
  text-align: center;
}
#b5 {
  width: 35%;
  text-align: center;
}
#b2 {
  width: 16%;
  text-align: center;
}
#b3 {
  width: 15%;
  text-align: center;
}
#b4 {
  width: 15%;
  text-align: left;
}
</style>
