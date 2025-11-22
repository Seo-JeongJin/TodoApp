
<template>
  <ul>
    <li v-for="todo in todoList" :key="todo.id">
      {{ todo.msg }}
      <button type="button" @click="todoUpdate(todo.id)">Delete</button>
    </li>
  </ul>
</template>

<script>
  export default {
    props : ["todoList"], // 부모에서 케밥 케이스로 던지면 자식에선 카멜 케이스로 받기
    
    methods : {
      todoUpdate(id) {
        this.$emit("todoUpdate", id)
      }
    }
  }
</script>