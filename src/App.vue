<template>
  <div class="wraper">
    <div>第{{n}}步</div>
    <div>
      <div class="row">
        <Cell @click="onClickCell(0,$event)" :n="n" :res="result"></Cell>
        <Cell @click="onClickCell(1,$event)" :n="n" :res="result"></Cell>
        <Cell @click="onClickCell(2,$event)" :n="n" :res="result"></Cell>
      </div>
      <div class="row">
        <Cell @click="onClickCell(3,$event)" :n="n" :res="result"></Cell>
        <Cell @click="onClickCell(4,$event)" :n="n" :res="result"></Cell>
        <Cell @click="onClickCell(5,$event)" :n="n" :res="result"></Cell>
      </div>
      <div class="row">
        <Cell @click="onClickCell(6,$event)" :n="n" :res="result"></Cell>
        <Cell @click="onClickCell(7,$event)" :n="n" :res="result"></Cell>
        <Cell @click="onClickCell(8,$event)" :n="n" :res="result"></Cell>
      </div>
    </div>

    <div>{{map}}</div>
    <div v-if="result">
      {{result}}
      <button @click="reset">重新开始</button>
    </div>
  </div>
</template>

<script>
import Cell from "./components/Cell";
export default {
  components: { Cell },
  data() {
    return {
      n: 0,
      map: [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ],

      result: false
    };
  },
  methods: {
    onClickCell(i, text) {
      console.log(`${i}号被点击了,内容是${text}`);
      i;
      // 0 map[0,0]
      // 1 map[0,1]
      // 2 map[0,2]
      // 3 map[1,0]
      // 4 map[1,1]
      // 5 map[1,2]
      // 6 map[2,0]
      // 7 map[2,1]
      // 8 map[2,2]

      this.map[Math.floor(i / 3)][i % 3] = text;
      this.n = this.n + 1;
      this.tell();
    },
    reset() {
      console.log(this.$children);
      this.$children.map(item => {
        item.status = false;
        item.text = "";
      });
      this.map = [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ];
      this.result = false;
      this.n = 0;
    },
    tell() {
      let map = this.map;
      console.log(map);
      for (let i = 0; i <= 2; i++) {
        if (
          map[i][0] !== null &&
          map[i][0] === map[i][1] &&
          map[i][1] === map[i][2]
        ) {
          this.result = map[i][0] + "胜利";
        }
      }
      for (let j = 0; j <= 2; j++) {
        if (
          map[0][j] !== null &&
          map[0][j] === map[1][j] &&
          map[1][j] === map[2][j]
        ) {
          this.result = map[0][j] + "胜利";
        }
      }

      if (
        map[0][0] !== null &&
        map[0][0] == map[1][1] &&
        map[1][1] == map[2][2]
      ) {
        this.result = map[0][0] + "胜利";
      }
      if (
        map[0][2] !== null &&
        map[0][2] == map[1][1] &&
        map[1][1] == map[2][0]
      ) {
        this.result = map[0][2] + "胜利";
      }
      if (map.flat(2).every(item => item !== null)) {
        this.result = "平局";
      }
    }
  }
};
</script>

<style>
.row {
  display: flex;
}
.wraper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>