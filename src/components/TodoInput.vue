
<!-- 내가 이해한 대로 동작한 과정 설명
사용자가 input 태그에 메세지를 입력하면 v-model 로 인하여 양방향 바인딩이 되기에 msg에 사용자가 값을 넣는대로 msg 값이 즉시 바뀜. 
메세지를 입력하고 사용자가 버튼을 클릭하면 todoInput 메서드 실행됨. 
todoInput 메서드 실행으로 인해 todoInput 이라는 이벤트가 this.msg 값을 함께 가지고 부모 컴포넌트로 전달됨. 
그 후에 바로 msg 값은 초기화 됨. -->

<template>
  <!-- 엔터로도 할 일 추가 하고 싶은데 브라우저 기본 submit 때문에 새로고침 되는 문제 발생
  Vue 에서는 form의 submit 이벤트를 잡아서 처리할 수 있음
  @submit="todoInput" -> submit 이벤트가 발생하면 todoInput 메서드 실행
  .prevent -> 내부적으로 event.preventDefault() 호출 -> 페이지 새로고침 막음 -->
  <form @submit.prevent="todoInput">
    <input type="text" placeholder="Enter a new task" v-model="msg">
    <button type="button" @click="todoInput">Add</button>
    <p v-if="errorMessage" style="color: red;">
      {{ errorMessage }}
    </p>
  </form>
</template>

<script>
  export default {

    data() {
      return {
        msg : '',
        errorMessage : ''
      }
    },

    methods : {
      todoInput() {
        if (!this.msg.trim()) { // trim() === 문자열의 앞 뒤 공백 제거 메서드
          this.errorMessage = 'Please enter your task!'
          return; // this.msg.trim() 의 값이 빈 문자열(false)이면 해당 메서드 종료 
        } 
        
        // 정상 입력일 경우 에러 메세지 제거
        this.errorMessage = '';

        this.$emit("todoInput", this.msg); // todoInput 이벤트를 this.msg 와 함께 부모 컴포넌트로 전달
        this.msg = '';
      }
    }

  }
</script>