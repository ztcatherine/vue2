<template>
  <div id="app-continer">
    <div id="wrap">
      <app-header :addTodo="addTodo"></app-header>
      <list :todos="todos"></list>
      <app-footer :selectAll="selectAll" :clearAll="clearAll" :todos="todos"></app-footer>
    </div>
  </div>
</template>

<script>
  import header from './header.vue'
  import list from './list.vue'
  import footer from './footer.vue'
  import PubSub from 'pubsub-js'
  export default {
    data(){
      return{
        todos:[]
      }
    },
    mounted(){
      this.todos=JSON.parse(localStorage.getItem('todos_key')||'[]')
      /*订阅消息*/
      PubSub.subscribe('deleteTodo',(msg,index)=>{
        //console.log(msg,index)
        this.deleteTodo(index)
      })
    },
    methods:{
      addTodo(todo){
        this.todos.unshift(todo)
      },

      deleteTodo(index){
        this.todos.splice(index,1)
      },
       /*  全选  */
      selectAll(isCheck){
        this.todos.forEach(todo=>{
          todo.checked=isCheck
        })
      },

      /*  清除选中的  */
      clearAll(){
        this.todos=this.todos.filter(todo=>!todo.checked)
      }
    },

    watch:{
      todos:{
        deep:true,
        handler:function (value) {
          localStorage.setItem('todos_key',JSON.stringify(value))
        }
      }
    },
    components:{
      'app-header': header,
      list,
      'app-footer':footer
    }
  }
</script>

<style>
  *{
    margin: 0;
    padding: 0;
  }
  html,body{
    width: 100%;
    height: 100%;
  }
  /*app*/
  #app-continer{
    width: 600px;
    margin: 0 auto;
  }
  #wrap{
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
