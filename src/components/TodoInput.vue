
<!-- 내가 이해한 대로 동작한 과정 설명
사용자가 input 태그에 메세지를 입력하면 v-model 로 인하여 양방향 바인딩이 되기에 msg에 사용자가 값을 넣는대로 msg 값이 즉시 바뀜. 
메세지를 입력하고 사용자가 버튼을 클릭하면 todoInput 메서드 실행됨. 
todoInput 메서드 실행으로 인해 todoInput 이라는 이벤트가 this.msg 값을 함께 가지고 부모 컴포넌트로 전달됨. 
그 후에 바로 msg 값은 초기화 됨. -->

<template>
  <form id="todo-form">
    <input type="text" id="todo-input" 
    placeholder="Enter a new task" v-model="msg">
    <button type="button" @click="todoInput">Add</button>
  </form>
</template>

<script>
  export default {
    data() {
      return {
        msg : '',
      }
    },
    methods : {
      todoInput() {
        this.$emit("todoInput", this.msg); // todoInput 이벤트를 this.msg 와 함께 부모 컴포넌트로 전달
        this.msg = '';
      }
    }
  }
</script>

<style>

</style>