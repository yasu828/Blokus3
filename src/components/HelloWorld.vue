<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1> -->
    <slot name="message"></slot>
    <h3>{{ messe }}</h3>
    <h3>{{ username }}</h3>
    <p><button @click="increment">+1</button> {{ count }} </p>
    <div>
      <label for="condition">元気？</label>
      <input type="text" id="condition" :value="value" @input="$emit('input', $event.target.value)">
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      name: 'HelloWorld',
      messe: "おはよう！！",
      count: 0,
    }
  },
  props: {
    username: String,
    value: String
  },
  methods: {
    increment(){
        this.count += 1;
        this.$emit("add",this.count);
    },
  }
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
