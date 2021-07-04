<template>
  <div id="app">
    <BlokusHeader class="header"></BlokusHeader>
    <LeftPlayersBlock1 
    class="player1"
    @click="handClick"
    @click2="turnLeft"
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
import BlokusHeader from './components/BlokusHeader.vue'
export default {
  components: {
    BlokusHeader,
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
    turnLeft(chooseBlock) {
      this.item = chooseBlock
    },
    droped(x, y){
      const itemRow = this.item.length;
      const itemCell = this.item[0].length;
      for (let i = 0; i < itemRow; i++) {
        for (let j = 0; j < itemCell; j++) {
          if (this.mainBoard[y + i][x + j].code == 0) {
            this.mainBoard[y + i][x + j].code = this.item[i][j].code;
          }
        }
      }
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
	background-color: rgba(123, 113, 102, 0.6);
	background-image:radial-gradient(#5a5e59 1px, transparent 1px);
	background-size: 20px 20px;
  display: grid;
  height: 100vh;
  grid-template: 
  "top  top  top  top  top  top  top"  12%
  ".... .... .... .... .... .... ...." 3%
  ".... p1   main main main p3   ...." 42%
  ".... .... main main main ...  ...." 1%
  ".... p2   main main main p4   ...." 42%
  /10px 1fr  2fr  2fr  2fr  1fr  10px;
}
// grid-areaここから
.header{
  grid-area: top;
}
.table{
  grid-area: main;
  background-color: white;
  height: 91%;
  border: black solid 3px;
  margin: auto;
}
.player1{
  grid-area: p1;
  margin: auto;
}
.player2{
  grid-area: p2;
  display: flex;
  margin: auto;
}
.player3{
  grid-area: p3;
  display: flex;
  margin: auto;
}
.player4{
  grid-area: p4;
  display: flex;
  margin: auto;
}
// grid-areaここまで

.MainTableCell{
  height: 20px;
  width: 20px;
  border: solid black 1px;
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

.chooseblocks{
  height: 120px;
  width: 120px;
  background-color: beige;
}
</style>