<template>
  <div id="app">
    <LeftPlayersBlock 
    class="player1"
    @click="handClick3"
    >
    </LeftPlayersBlock>

    <LeftPlayersBlock 
    class="player2"
    @click="handClick3"
    >
    </LeftPlayersBlock>

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

    <RightPlayersBlock 
    class="player3"
    @click="handClick3"
    >
    </RightPlayersBlock>
    
    <RightPlayersBlock 
    class="player4"
    @click="handClick4"
    >
    </RightPlayersBlock>
  </div>
</template>

<script>

import RightPlayersBlock from './components/RightPlayersBlock.vue'
import LeftPlayersBlock from './components/LeftPlayersBlock.vue'
// import "./style.scss";
export default {
  components: {
    RightPlayersBlock,
    LeftPlayersBlock,
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
      item1: [],
      item2: [],
      item3: [],
      item4: [],
    };
  },
  methods:{
    handClick3(chooseBlock){
      this.item3 = chooseBlock
    },
    handClick4(chooseBlock){
      this.item4 = chooseBlock
    },
    droped(x, y){
      if (this.item3.length == 5) {
        for (let i = 0; i < 5; i++) {
          for (let j = 0; j < 5; j++) {
            this.mainBoard[y + i][x + j].code = this.item3[i][j].code;
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

.is-2{
  background-color: blueviolet;
}
.is-1{
  background-color: rgb(43, 144, 226);
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