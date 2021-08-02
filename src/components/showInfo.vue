<template>
  <div>
    <button @click="init">点此展示记录</button>
    <ul class="itemMain">
      <infoItem class="infoItem" v-for="item in items"
      :key="item._id" 
      :item="item" />
    </ul>
  </div>
</template>

<script>
import infoItem from "@/components/infoItem";
export default {
  mounted(){
    this.$bus.$on("initShow", this.init)
  },
  components: {
    infoItem,
  },
  methods: {
    init(){
      this.$bus.$emit('initItem')
      this.$bus.$emit('tableInit')
      // this.$bus.$emit("tableInit");
    }
  },
  props: ["items"],
};
</script>

<style scoped>
ul{
  
}

	.itemMain {
		margin-left: 0px;
		border: 1px solid #ddd;
		border-radius: 2px;
		padding: 10px;
    /* overflow: scroll; */
	}
.infoItem{
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
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
}
</style>
