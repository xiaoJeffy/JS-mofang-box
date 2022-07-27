<template>
  <div class="hello">
    <button @click="showToggle">显示子组件</button>
    <button @click="hideToggle">隐藏子组件</button>
    <div v-show="isshow" class="flex-box">
      <div class="flex-item" :class="item.color" v-for="item in list">{{item.text}}</div>
      <button @click="clockwise">顺时针旋转一格</button>
      <button @click="start">开始抽奖</button>
      <button @click="ending">结束抽奖</button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data(){
    return{
      list:[
        {id:1,text:1,color:"pink"},
        {id:2,text:2,color:"grey"},
        {id:3,text:3,color:"green"},
        {id:4,text:4,color:"yellow"},
        {id:5,text:'',color:"white"},
        {id:6,text:5,color:"purple"},
        {id:7,text:"abc",color:"orange"},
        {id:8,text:"d",color:"wheat"},
        {id:9,text:"e",color:"blue"},
      ],
      text:"显示",
      isshow:false,
      btnText:"隐藏",
      timer:null
    }
  },
  /*mounted() {
    this.helloworld()
  },*/
  methods:{
    showToggle(){
      this.isshow =! this.isshow
      this.text = "隐藏"
      this.isshow = true
    },
    hideToggle(){
      this.isshow =! this.isshow
      this.btnText = "显示"
      this.isshow = false
    },
    change(arr){
      let [a,b,c,d,e,f,g,h,i]=[...arr];
      [a,b,c,d,e,f,g,h,i]=[d,a,b,g,e,c,h,i,f]
      return [a,b,c,d,e,f,g,h,i]
    },
    clockwise(){
      this.list = this.change(this.list)
    },
    start(){
      this.list[4].text=''
      this.list[4].color="white"
      let self = this
      if(this.timer==null)
      {
        this.timer = setInterval(function(){
          self.clockwise()
        },100)
      }
      else{
        clearInterval(this.timer)
        this.timer = setInterval(function(){
          self.clockwise()
        },100)
      }
    },
    ending(){
      clearInterval(this.timer)
      this.list[4].text="中奖号"+this.list[1].text;
      this.list[4].color="red"
    }
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
* {
  margin:0;
  padding:0;
}
.flex-box
  {
      width: 500px;
      height: 500px;
      background-color: #FFFFFF;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-evenly;
      margin-top: 50px;
      margin-left: 500px;
  }
  .flex-item
  {
    width: 150px;
    height: 150px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .pink {
    background-color: #FFC0CB;
  }
  .grey {
    background-color: #808080;
  }
  .green{
    background-color: #008000;
  }
  .yellow {
    background-color: #FFFF00;
  }
  .purple {
    background-color: #800080;
  }
  .orange{
    background-color: #FFA500;
  }
  .wheat {
    background-color: #F5DEB3;
  }
  .blue {
    background-color: #0000FF;
  }
  .red{
    background-color: red ;
    color:yellow;
    font-size: 20px;
  }
</style>