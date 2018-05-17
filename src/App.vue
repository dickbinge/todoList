<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input  v-model="newItem" @keyup.enter="addNewItem"/>
    <ol>
      <li v-for="item in items" v-bind:class="{isFinished:item.isFinished}" v-on:click='toggleFinsh(item)'>{{item.label}}</li>
    </ol>
    <div style="height:100px; width:1px; border-left:1px #000 solid"></div>
    <p>child tells Me:{{childWord}}</p>
    <component-a msgfromFather="你是谁！" v-on:child-tell-me="letMeSay"></component-a>
  </div>

</template>

<script>
import Store from './store.js'
import ComponentA from './components/componentA'
export default {
  name: 'App',
  data:function(){
    return{
        title:'this is  a todo list!',
        items:Store.fetch()==null?[]:Store.fetch(),  //items 的值原本是自定义的，现在需要从window.localStorage.getItem('todos-vuejs')
        newItem:'',
        childWord:''
    }
  },
  components:{ComponentA},    //必须写props，否则无法接受到，接收到的一直是undefined
  watch:{
      items:{
          handler:function(items){
              Store.save(items)
          },
          deep:true
      }
  },
  methods:{
      toggleFinsh:function(item){
          item.isFinished=!item.isFinished
      },
      addNewItem:function(){
          this.items.push({
              label:this.newItem,
              isFinished:false
          }),
          this.newItem=''
      },
      letMeSay:function(msg){
          console.log(msg)
          this.childWord=msg
      }
  }
  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.isFinished{
   text-decoration:line-through;
   font-style:italic;
   color:#C0C0C0;
}
li{
   width:100px;
   margin:auto;
   margin-top: 10px;
   font-size: 1.6em;
}
input{
  width:230px;
  height:40px;
  border-radius:20px;
  padding: 0.4em 0.35em;
  border:3px solid #CFCFCF;
  font-size: 1.55em;
}
</style>
