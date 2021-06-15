<template>
  <div id="app">
    <table>
      <draggable 
        tag="tr" 
        v-for="(boardRow, y) in mainBoard" 
        :key="y"
      >
        <draggable
          tag="td" 
          class="MainTableCell" 
          v-for="(cell, x) in boardRow" 
          :key="x" 
          :class="`is-${cell.code}`" 
        >
        </draggable>
      </draggable>
    </table>

    <draggable 
      tag="div" 
      v-for="(block, bi) in blocks" 
      :key="bi"
    >
      <table>
        <tr v-for="(blockTR, yi) in block" :key="yi">
          <td 
            class="blockCell"
            v-for="(blockTD, xi) in blockTR" 
            :key="xi"
            :class="`is-${blockTD.code}`"
          ></td>
        </tr>
      </table>
    </draggable>
  <p>
    {{namsa}}
  </p>
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
      [
        [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
        [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
        [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
        [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
        [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ],
      [
        [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
        [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
        [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
        [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
        [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ],
    ];
    const mainBoard = []
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
    const draggable = window['vuedraggable'];
// ここからvue.js記述
    return{
      namsa:"hello",
      components: {
        'draggable': draggable,
      },
      TD:"TD",
      message:"",
      mainBoard: mainBoard,
      blocks:blocks
    };
  },
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
}

.MainTableCell{
    height: 20px;
    width: 20px;
    border: solid black 1px;
}

.blockCell{
    height: 20px;
    width: 20px;
}

.is-2{
    background-color: blueviolet;
}
.is-1{
    background-color: rgb(43, 144, 226);
}
</style>
