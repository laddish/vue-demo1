<template>
  <div class="cell" @click="onClickSelf">
    <template v-if="status">
      <icon-svg class="cellicon" :icon-class="text" />
    </template>
    <template v-else></template>
  </div>
</template>

<script>
import IconSvg from "@/components/IconSvg";

export default {
  props: ["n", "res"],
  components: { IconSvg },

  data() {
    return {
      status: false,
      text: ""
    };
  },
  // computed: {
  //   // 永远会随着n的变化而变化
  //   text() {
  //     return n % 2 == 0 ? "x" : "o";
  //   }
  // },
  methods: {
    onClickSelf() {
      console.log(this.res);
      if (this.text !== "" || this.res) {
        return;
      }
      this.status = true;
      this.text = this.n % 2 === 0 ? "zu" : "yuan";
      this.$emit("click", this.text);
    }
  }
};
</script>

<style>
.cell {
  border: 1px solid black;
  width: 100px;
  height: 100px;
  font-size: 50px;
  vertical-align: bottom;
  display: flex;
  justify-content: center;
  align-content: center;
  user-select: none;
}
.cellicon {
  margin: auto;
}
</style>
