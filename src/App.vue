<template>
<div>
  <input type="text" v-model="val">
  <button @click="addTodo">添加</button>
  <button @click="delTodo">清理</button>
  <ul v-if="todos.length">
    <li v-for="(todo,index) in todos ">
      <input v-model="todo.done" type="checkbox">
      <span :class="{done:todo.done}">
        {{ todo.title }}
      </span>
      <span @click="removeTodo(index)">
        🗑
      </span>
    </li>
  </ul>
  <div v-else>暂无数据</div>
  <div>
    全选
    <input id="" v-model="allDone" name="全选" type="checkbox">
    <span>{{ active }}/{{ all }}</span>
  </div>
</div>
</template>
<script lang="ts" setup>
import {ref, Ref, computed} from 'vue'

interface Todo {
  title: string,
  done: boolean
}

let val = ref<string>('')
let todos = ref<Todo[]>([{
  title: '吃饭',
  done: true
}, {
  title: '睡觉',
  done: false
}, {
  title: '学习',
  done: false
}])

function addTodo() {
  todos.value.push({
    title: val.value,
    done: false
  })
  val.value = ''
}

function removeTodo(index: number) {
  todos.value.splice(index, 1)
}

function delTodo() {
  todos.value = todos.value.filter(v => !v.done)
}

// let allDone = ref(false)
let active = computed<number>(() => todos.value.filter(v => v.done).length)
let all = computed<number>(() => todos.value.length)
let allDone = computed<boolean>({
  get() {
    return active.value === todos.value.length
  },
  set(value: boolean) {
    todos.value.forEach((todo) => {
      todo.done = value
    })
  }
})
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
span.done {
  text-decoration: line-through;
  color: gray;
}
</style>
