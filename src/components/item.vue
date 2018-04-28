<template>
  <li @mouseenter="handleEnter(true)" @mouseleave="handleEnter(false)" :style="{background:'bgColor'}">
    <label>
      <input type="checkbox" v-model="todo.checked"/>
      <span>{{todo.title}}</span>
    </label>
    <button class="btn" v-show="isShow" @click="deleteItem">删除</button>
  </li>
</template>

<script>
  import PubSub from 'pubsub-js'
  export default {
    props:{
      todo:Object,
      index:Number
    },
    data(){
      return{
        isShow:false,
        bgcolor:'white'
      }
    },

    methods:{
      handleEnter(isEnter){
        if(isEnter){
          this.isShow=true
          this.bgColor='gray'
        }else {
          this.isShow=false
          this.bgColor='white'
        }
      },

      deleteItem(){
        //this.deleteTodo(this.index)
        //发布消息
        PubSub.publish('deleteTodo',this.index)
      }
    }
  }
</script>

<style>
  /*item*/
  li{
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }
  li label{
    float: left;
    cursor: pointer;
  }
  li label li input{
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }
  li button{
    display: inline-block;
    float: right;
    margin-top: 3px;
  }
  li:before{
    content: initial;
  }
  li:last-child{
    border-bottom: none;
  }
</style>
