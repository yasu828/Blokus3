<template>
  <div class="p4">
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
        <button @click.prevent @click="turnLeft()">左に回転
        </button>
        <button @click.prevent @click="turnRight()">右に回転
        </button>
        <button @click.prevent @click="Inversion()">反転
        </button>
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

    return{
        blocks:blocks,
        haveItem: [],
        chooseBlock: chooseBlock,
    }
  },
  methods: {
    turnLeft(){
      this.haveItem = JSON.parse(JSON.stringify(this.chooseBlock))
      for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 5; j++) {
          this.chooseBlock[4 - i][j].code = this.haveItem[j][i].code
        }
      }
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
      this.item = this.blocks.find(x=>x.name==block.name).data;
      for (let i = 0; i < 5; i++) {
        for (let j = 0; j < 5; j++) {
          this.chooseBlock[i][j].code = this.item[i][j].code
        }
      }
      this.$emit("click",this.chooseBlock);
    },
  }
}
</script>

<style scoped>
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

.handBlock{
  height: 200px;
  width: 320px;
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
</style>
