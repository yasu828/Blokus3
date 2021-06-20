<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1> -->
    <h3>{{ messe }}</h3>
    <h3>{{ username }}</h3>
  </div>
</template>

<script>
export default {
  data(){
    return{
      name: 'HelloWorld',
      messe: "おはよう！！"
    }
  },
  props: {
    username: String
  },
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
  color: deeppink;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
