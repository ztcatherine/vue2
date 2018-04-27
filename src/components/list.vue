<template>
  <ul class="app-main">
    <item v-for="(todo,index) in todos" :key="index" :todo="todo" :deleteTodo="deleteTodo" :index="index"></item>
  </ul>
</template>

<script>
  import item from './item.vue'
  export default {
    props:{
      todos:Array,
      deleteTodo:Function
    },
    components:{
      item
    }
  }
</script>

<style>
  .app-main{
    margin-left: 0;
    border: 1px solid #ddd;
  }
</style>
