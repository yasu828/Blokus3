<template>
  <div class="p1">
    <div class="handBlock">
      <div 
        v-for="(block, bi) in blocks" 
        :key="bi" 
        group="items" 
        @click="handClick(block)"
      >
        <table class="handTable">
          <tr v-for="(blockTR, yi) in block.data" :key="yi">
            <td 
              class="handBlockCell" 
              v-for="(blockTD, xi) in blockTR" 
              :key="xi" 
              :class="`is-${blockTD.code}`"
            >
            </td>
          </tr>
        </table>
      </div>
    </div>
    <div>
      <div class="chooseblocks">
        <draggable>
          <table>
            <tr 
              v-for="(chooseBlockRow, vi) in chooseBlock"
              :key="vi">
              <td 
                class="blockCell2"
                v-for="(chooseBlockCell, mi) in chooseBlockRow" 
                :key="mi"
                :class="`is-${chooseBlockCell.code}`">
              </td>
            </tr>
          </table>
        </draggable>
      </div>
      <div class="btn">
          <!-- 入れる配列をみて初めに0以外の数字がきたところを取得し、そこから配列データを受け皿に入れる。
          もしくは5x5ではなくブロックごとに必要なだけの配列でそれぞれ作成する。 -->
        <button class="left-btn" @click.prevent @click="turnLeft()">左回転
        </button>
        <button class="right-btn" @click.prevent @click="turnRight()">右回転
        </button>
        <button @click.prevent @click="Inversion()">反転
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
export default {
    components: {
    draggable,
    },
  data(){
    const blocks = [
      { name:0,
        data:[
          [{code:1}],
      ]},
      // 数字の配列をオブジェクトの配列に変換する
      { name:1,
        data:[
          [{code:1}],
          [{code:1}],
      ]},
      { name:2,
        data:[
          [{code:1}, {code:0}],
          [{code:1}, {code:1}],
      ]},
      { name:3,
        data:[
          [{code:1}, {code:1}, {code:1}],
      ]},
      { name:4,
        data:[
          [{code:1}, {code:1}],
          [{code:1}, {code:1}],
      ]},
      { name:5,
        data:[
          [{code:1}, {code:0}],
          [{code:1}, {code:1}],
          [{code:1}, {code:0}],
      ]},
      { name:6,
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}],
      ]},
      { name:7,
        data:[
          [{code:1}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}],
      ]},
      { name:8,
        data:[
          [{code:1}, {code:0}],
          [{code:1}, {code:1}],
          [{code:0}, {code:1}],
      ]},
      { name:9,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:1}],
      ]},
      { name:10,
        data:[
          [{code:1}, {code:1}, {code:1}],
          [{code:0}, {code:1}, {code:0}],
          [{code:0}, {code:1}, {code:0}],
      ]},
      { name:11,
        data:[
          [{code:1}, {code:0}, {code:0}],
          [{code:1}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}],
      ]},
      { name:12,
        data:[
          [{code:1}, {code:0}],
          [{code:1}, {code:1}],
          [{code:0}, {code:1}],
          [{code:0}, {code:1}],
      ]},
      { name:13,
        data:[
          [{code:1}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}],
          [{code:0}, {code:0}, {code:1}],
      ]},
      { name:14,
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:1}],
      ]},
      { name:15,
        data:[
          [{code:1}, {code:0}],
          [{code:1}, {code:1}],
          [{code:1}, {code:1}],
      ]},
      { name:16,
        data:[
          [{code:1}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}],
          [{code:0}, {code:1}, {code:1}],
      ]},
      { name:17,
        data:[
          [{code:1}, {code:1}],
          [{code:1}, {code:0}],
          [{code:1}, {code:1}],
      ]},
      { name:18,
        data:[
          [{code:0}, {code:1}, {code:1}],
          [{code:1}, {code:1}, {code:0}],
          [{code:0}, {code:1}, {code:0}],
      ]},
      { name:19,
        data:[
          [{code:0}, {code:1}, {code:0}],
          [{code:1}, {code:1}, {code:1}],
          [{code:0}, {code:1}, {code:0}],
      ]},
      { name:20,
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}],
          [{code:0}, {code:1}, {code:0}, {code:0}],
      ]},
    ];
    // const chooseBlock = [];
    //   for (let y = 0; y < 5; y++ ) {
    //     const chooseBlockRow = []
    //     for (let x = 0; x < 5; x++){
    //       const chooseBlockCell = {
    //         y: y,
    //         x: x,
    //         code: 0,
    //       };
    //     chooseBlockRow.push(chooseBlockCell)
    //   }
    //   chooseBlock.push(chooseBlockRow)
    //   }
// propsをつかうchooseBlockCell{}にAppからデータを入れたい
    return{
        blocks:blocks,
        haveItem: [],
        chooseBlock: [],
        testhave: [],
        // blockdata:{
        //   y: y,
        //   x: x,
        //   code:""
        // },
    }
  },
  methods: {
    turnLeft(){
      // データのコピーをする
      this.haveItem = JSON.parse(JSON.stringify(this.chooseBlock))
      const haveRow = this.haveItem.length;
      const haveCOL = this.haveItem[0].length;
      const col = haveCOL-1;
      const Turnchoose = []
      for (let x = 0; x < haveCOL; x++) {
        const TurnBlockRow = []
        for (let y = 0; y < haveRow; y++) {
          const num = this.haveItem[y][col-x].code
          const TurnBlockCell = {
            y: y,
            x: x,
            code: num,
          };
        TurnBlockRow.push(TurnBlockCell)
        }
      Turnchoose.push(TurnBlockRow)
      }
      this.chooseBlock = Turnchoose
      this.$emit("click2",this.chooseBlock);
      // this.$emit("click2",this.chooseBlock);
    },
    turnRight(){
      this.haveItem = JSON.parse(JSON.stringify(this.chooseBlock))
      for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 5; j++) {
          this.chooseBlock[i][4 - j].code = this.haveItem[j][i].code
        }
      }
    },
    Inversion(){
      this.haveItem = JSON.parse(JSON.stringify(this.chooseBlock))
      for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 5; j++) {
          this.chooseBlock[i][j].code = this.haveItem[j][i].code
        }
      }
    },
    handClick(block){
      this.chooseBlock = this.blocks.find(x=>x.name==block.name).data;
      for (let i = 0; i < this.chooseBlock.lenght; i++) {
        for (let j = 0; j < this.chooseBlock[i].lenght; j++) {
          this.chooseBlock = this.item[i][j].code
        }
      }
      this.$emit("click",this.chooseBlock);
    },
  }
}
</script>

<style scoped lang="scss">
.p1{
  display: flex;
}
.handBlockCell{
  height: 6px;
  width: 6px;
}

.handTable{
  margin: 5px;
}

.blockCell2{
  height: 20px;
  width: 20px;
}

.is-1{
  background-color: rgb(10, 241, 29);
}

.handBlock{
  height: 100%;
  width: 280px;
  display: flex;
  flex-wrap: wrap;
  border: rgb(10, 241, 29) 2px solid;
  background-color: rgb(238, 255, 239);
}

.chooseblocks{
  height: 120px;
  width: 120px;
  background-color: beige;
  border: rgb(10, 241, 29) 1px solid;
}

.btn{
  display: flex;
  width: 100%;
  &.left-btn{
    width: 50%;
  }
  &.right-btn{
    width: 50%;
  }
}
</style>
