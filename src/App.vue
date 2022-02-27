<template>
<div>
  {{ val }}
  <input type="text" v-model="val">
  <button @click="addTodo">添加</button>
  <ul>
    <li v-for="todo in todos ">
      {{todo}}
    </li>
  </ul>
</div>
</template>
<script lang="ts" setup>
  import {ref} from 'vue'
  let val =ref('')
  let todos = ref(['吃饭','睡觉','学习!!'])
  function addTodo () {
    todos.value.push(val.value)
    val.value = ''
  }
// export  default  {
  //
  // setup(){
  //   let val =ref('')
  //   return {
  //     val
  //   }
  // }
// }
// export default {
//   data(){
//     return {
//       count:1
//     }
//   },
//   methods:{
//     add(){
//       this.count++
//     }
//   }
// }
</script>

<style>

</style>
