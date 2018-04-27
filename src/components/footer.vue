<template>
  <div id="app-footer">
    <label>
      <input type="checkbox" v-model="isAllChecked">
    </label>
    <span>
            <span>已完成{{checkedSize}}</span> / 全部{{todos.length}}
          </span>
    <button class="btn" v-show="checkedSize" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    props:['todos','clearAll','selectAll'],
    computed:{
      checkedSize(){
        return this.todos.reduce((preTotal,todo)=>{
          return preTotal + (todo.checked ? 1 : 0)
        },0)
      },



      isAllChecked:{
        get () {
          return this.checkedSize===this.todos.length && this.todos.length>0
        },
        set(value){
          this.selectAll(value)
        }
      }
    }
  }
</script>

<style>
  /*footer*/
  #app-footer{
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }
  #app-footer label{
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }
  #app-footer label input{
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }
  #app-footer button{
    float: right;
    margin-top: 5px;
  }
</style>
