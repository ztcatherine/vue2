<template>
  <ul class="app-main">
    <item v-for="(todo,index) in todos" :key="index" :todo="todo" :index="index"></item>
  </ul>
</template>

<script>
  import item from './item.vue'
  export default {
    props:{
      todos:Array
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
