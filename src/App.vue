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
          @drop="droped(cell)"
        >
        </td>
      </tr>
    </table>

    <draggable div
      v-for="(block, bi) in blocks" 
      :key="bi"
      group="items"
      @start="dragstart(block)"
      @end="onEnd(block)"
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
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p2",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p3",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p4",
        data:[
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p5",
        data:[
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p6",
        data:[
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p7",
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p8",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p9",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p10",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p11",
        data:[
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p12",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p13",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p14",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p15",
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:1}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p16",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p17",
        data:[
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p18",
        data:[
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p19",
        data:[
          [{code:0}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p20",
        data:[
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:1}, {code:1}, {code:1}, {code:0}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
      ]},
      { name:"p21",
        data:[
          [{code:1}, {code:1}, {code:1}, {code:1}, {code:0}],
          [{code:0}, {code:1}, {code:0}, {code:0}, {code:0}],
          [{code:0}, {code:0}, {code:0}, {code:0}, {code:0}],
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
      dragName: "",
    };
  },
  methods:{
    beforeMove: function(evt) {
      return evt.draggedContext.element.name !== 'fild';
    },
    dragstart(block){
      this.dragItem = block.name;
    },
    onEnd(block){
      block.name = this.dragName;
    },
    droped(cell){
      switch(this.dragItem){
        case "p1":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p2":
          this.dragName = this.dragItem;
          this.mainBoard[cell.y][cell.x].code = 1
          this.mainBoard[cell.y = cell.y + 1][cell.x].code = 1
        break;
        case "p3":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p4":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p5":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p6":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p7":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p8":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p9":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p10":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p11":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p12":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p13":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p14":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p15":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p16":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p17":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p18":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p19":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p20":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
        case "p21":
          this.mainBoard[cell.y][cell.x].code = 1
          this.dragItem = "";
        break;
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