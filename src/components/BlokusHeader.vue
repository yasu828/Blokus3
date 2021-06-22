<template>
  <div class="blokus-header">
    {{ title }}
  </div>
</template>

<script>
export default {
  data(){
    return{
      title:"Blokus3"
    }
  },
}
</script>

<style scoped>
.blokus-header{
  background-color: rgba(91, 159, 180, 0.973);
  border-bottom: rgb(0, 0, 0) solid 1px;
  height: 100%;
    color: whitesmoke;
  font-family: HanziPen SC;
  font-size:300%;
}
</style>
