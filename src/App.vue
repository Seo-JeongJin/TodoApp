
<template>
  <div>
    <h1>TODO List</h1>
    
    <!-- TodoInput 자식 컴포넌트에서 'todoInput' 이벤트가 emit되었을 때
    부모 컴포넌트의 todoInput 메서드를 실행하라 (자식으로부터 넘어온 이벤트는 케밥 케이스로 작성되어야 함) -->
    <TodoInput @todo-input="todoInput" />
    <!-- TodoList 라는 자식 컴포넌트에 todo-list 라는 props에 부모 컴포넌트에 있는 todoList 값을 넘긴다
    자식에게 props로 넘길 때는 케밥 케이스로 넘겨주고 자식 컴포넌트에서는 카멜 케이스로 받음 -->
    <TodoList :todo-list="todoList" @todo-update="todoUpdate"/>
   
  </div>
</template>

<script>
  import TodoInput from './components/TodoInput.vue';
  import TodoList from './components/TodoList.vue';
  import { v4 as uuidv4 } from 'uuid';

  export default {

    data() {
      return {
        todoList : []
      }
    },

    components : {
      TodoInput,
      TodoList
    },
    
    methods : {
      todoInput(msg) { // 자식이 보낸 this.msg 값을 사용하기 위해 인자를 받음(인자 이름은 하위 컴포넌트와 맞출 필요 당연히 없음)
        const item = {
          id : uuidv4(),
          msg : msg,
        }
        this.todoList.push(item);
      },
      todoUpdate(id) {
        // todoList 배열을 순회하며 각 항목(v)을 확인 -> v.id 가 부모로부터 emit된 id와 일치하지 않으면 남기고
        // 일치하지 않으면 제거 -> 이렇게 필터링된 새로운 배열을 todoLis에 다시 할당
        this.todoList = this.todoList.filter(v => v.id !== id)
      }
    }

  }
</script>
