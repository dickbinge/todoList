<template>
  <div class="hello">
      <h1>{{msg}}</h1>
      <button @click="onClickMe" >Click ME</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'hello from component a!'
    }
  },
  props:['msgfromFather'], //不写是undefined
  methods:{
      onClickMe:function(){
          console.log(this.msgfromFather)
          this.$emit('child-tell-me',this.msg)
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
