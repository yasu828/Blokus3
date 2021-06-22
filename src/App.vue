<template>
  <div id="app">
    <LeftPlayersBlock1 
    class="player1"
    @click="handClick"
    >
    </LeftPlayersBlock1>

    <LeftPlayersBlock2 
    class="player2"
    @click="handClick"
    >
    </LeftPlayersBlock2>

    <!-- ブロックを配置する基盤 -->
    <div class="table">
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
    <!-- //ブロックを配置する基盤 -->

    <RightPlayersBlock1 
    class="player3"
    @click="handClick"
    >
    </RightPlayersBlock1>
    
    <RightPlayersBlock2 
    class="player4"
    @click="handClick"
    >
    </RightPlayersBlock2>
  </div>
</template>

<script>

import RightPlayersBlock1 from './components/RightPlayersBlock1.vue'
import RightPlayersBlock2 from './components/RightPlayersBlock2.vue'
import LeftPlayersBlock1 from './components/LeftPlayersBlock1.vue'
import LeftPlayersBlock2 from './components/LeftPlayersBlock2.vue'
// import "./style.scss";
export default {
  components: {
    RightPlayersBlock1,
    RightPlayersBlock2,
    LeftPlayersBlock1,
    LeftPlayersBlock2,
  },
  name: 'App',
  data (){
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
// ここからvue.js記述
    return{
      mainBoard: mainBoard,
      item: [],
    };
  },
  methods:{
    handClick(chooseBlock){
      this.item = chooseBlock
    },
    droped(x, y){
      for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 5; j++) {
          if (this.mainBoard[y + i][x + j].code < 1) {
            this.mainBoard[y + i][x + j].code = this.item[i][j].code;
          }
        }
      }
      this.item3 = []
    },
  }
}
</script>

<style scoped lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: grid;
  height: 600px;
  grid-template: 
  "... ... ... ... ..." 1fr
  "p1 main main main p3" 1fr
  "... main main main ..." 1fr
  "p2 main main main p4" 1fr
  "... ... ... ... ..." 1fr
  /1fr 1fr 1fr 1fr 1fr;
}

.table{
  grid-area: main;
}

.player1{
  grid-area: p1;
  display: flex;
}
.player2{
  grid-area: p2;
  display: flex;
}
.player3{
  grid-area: p3;
  display: flex;
}
.player4{
  grid-area: p4;
  display: flex;
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

.is-1{
    background-color: rgb(10, 241, 29);
}
.is-2{
    background-color: rgb(4, 73, 250);
}
.is-3{
    background-color: rgb(248, 29, 29);
}
.is-4{
    background-color: rgb(244, 181, 10);
}

.handBlock{
  height: 200px;
  width: 320px;
  display: flex;
  flex-wrap: wrap;
  border: black 1px solid;
}

.chooseblocks{
  height: 120px;
  width: 120px;
  background-color: beige;
}
</style>