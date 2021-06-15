<template>
  <div id="app">
    <table>
      <tr 
        v-for="(boardRow, y) in mainBoard" 
        :key="y"
      >
        <td 
          class="MainTableCell" 
          v-for="(cell, x) in boardRow" 
          :key="x" 
          :class="`is-${cell.code}`" 
          @dragover.prevent
          @dragenter.prevent
          @drop="droped(cell, y)"
          @click="onClick(cell, y)"
        >
        </td>
      </tr>
    </table>

    <draggable div
      v-for="(block, bi) in blocks" 
      :key="bi"
      group="items"
      @start="dragstart(block)"
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
    </draggable>
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
      { name:"p1",
        data:[
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p2",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
    ];
    const mainBoard = []
      for (let y = 0; y < 20; y++ ) {
        const boardRow = []
        for (let x = 0; x < 20; x++){
          const cell = {
            y: y,
            x: x,
            code: 0,
            name: "fild",
          };
          boardRow.push(cell)
        }
        mainBoard.push(boardRow)
      }
// ここからvue.js記述
    return{
      components: {
        'draggable': draggable,
      },
      mainBoard: mainBoard,
      blocks:blocks,
      dragItem: "",
    };
  },
  methods:{
    beforeMove: function(evt) {
      return evt.draggedContext.element.name !== 'fild';
    },
    dragstart(block){
      this.dragItem = block.name;
    },
    droped(cell, y){
      console.log(cell)
      console.log(y)

      if (this.dragItem == "p1"){
        // this.mainBoard[y][cell.x].code = 1
        this.mianBoard[y + 1][cell.x + 1].code = 1
      }
    },
    onClick(cell, y){
      console.log(this.mianBoard[y + 1][cell.x + 1].code)
    }
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