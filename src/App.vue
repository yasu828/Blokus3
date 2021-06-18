<template>
  <div id="app">
    <!-- ブロックを配置する基盤 -->
    <div>
      <table>
        <tr 
          v-for="(boardRow, y) in mainBoard" 
          :key="y"
        >
          <td 
            class="MainTableCell"
            group="items" 
            v-for="(cell, x) in boardRow" 
            :key="x" 
            :class="`is-${cell.code}`" 
            @dragover.prevent
            @dragenter.prevent
            @drop="droped(x, y)"
          >
          </td>
        </tr>
      </table>
    </div>
    <!--// 基盤 -->

    <!-- 選んだブロックの表示 -->
    <div class="chooseblocks">
      <draggable tag="table">
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
      </draggable>
      <button @click.prevent @click="turnRight()">右に回す
      </button>
    </div>
    <!--// 選んだブロックの表示 -->
    <!-- 手持ちのブロック -->
    <div class="handBlock">
      <div
        v-for="(block, bi) in blocks" 
        :key="bi"
        group="items"
        @click="handClick(block)"
      >
        <table>
          <tr v-for="(blockTR, yi) in block.data" :key="yi">
            <td 
              class="blockCell"
              v-for="(blockTD, xi) in blockTR" 
              :key="xi"
              :class="`is-${blockTD.code}`"
            >
            </td>
          </tr>
        </table>
      </div>
    </div>
    <!-- // 手持ちのブロック -->
  </div>
</template>

<script>
import draggable from 'vuedraggable'
export default {
  components: {
    draggable,
  },
  name: 'App',
  data (){
    const blocks = [
      { name:0,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:1,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:2,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:3,
        data:[
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:4,
        data:[
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:5,
        data:[
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:6,
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:7,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:8,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:9,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:10,
        data:[
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:11,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:12,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:13,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:14,
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:1}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:15,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:16,
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:17,
        data:[
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:18,
        data:[
          [{code:0}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:19,
        data:[
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:20,
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
    ];
    const mainBoard = [];
      for (let y = 0; y < 20; y++ ) {
        const boardRow = []
        for (let x = 0; x < 20; x++){
          const cell = {
            y: y,
            x: x,
            code: 0,
          };
          boardRow.push(cell)
        }
        mainBoard.push(boardRow)
      } 
    const chooseBlock = [];
      for (let y = 0; y < 5; y++ ) {
        const chooseBlockRow = []
        for (let x = 0; x < 5; x++){
          const chooseBlockCell = {
            y: y,
            x: x,
            code: 0,
          };
        chooseBlockRow.push(chooseBlockCell)
      }
      chooseBlock.push(chooseBlockRow)
      }
// ここからvue.js記述
    return{
      components: {
        'draggable': draggable,
      },
      mainBoard: mainBoard,
      blocks:blocks,
      dragItem: "",
      item: [],
      haveItem: "",
      chooseBlock: chooseBlock,
    };
  },
  methods:{
    turnRight(){
      this.haveItem = this.blocks[this.dragItem].data
      for (let j = 0; j < 5; j++) {
        for (let i = 0; i < 5; i++) { 
          this.chooseBlock[j][i].code = this.haveItem[4 - i][j].code;
        }
      }
    },
    handClick(block){
      this.dragItem = block.name;
      this.item = this.blocks.find(x=>x.name==block.name).data;
      for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 5; j++) {
          this.chooseBlock[i][j].code = this.item[i][j].code
        }
      }
    },
    droped(x, y){
      for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 5; j++) {
          if (this.item[i][j].code==1) {
            this.mainBoard[y + i][x + j].code = this.item[i][j].code
          }
        }
      }
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  height: 600px;
}

.MainTableCell{
    height: 20px;
    width: 20px;
    border: solid black 1px;
}

.blockCell{
    height: 6px;
    width: 6px;
}
.blockCell2{
    height: 16px;
    width: 16px;

}

.is-2{
    background-color: blueviolet;
}
.is-1{
    background-color: rgb(43, 144, 226);
}
.haveBlock{
  height: 500px;
  width: 150px;
  display: flex;
  flex-wrap: wrap;
}

.chooseblocks{
  height: 120px;
  width: 120px;
  background-color: beige;
}
</style>