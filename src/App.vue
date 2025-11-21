
<template>
  <div class="todo-container">
    <h1>TODO List</h1>
    
    <!-- TodoInput 자식 컴포넌트에서 'todoInput' 이벤트가 emit되었을 때
    부모 컴포넌트의 todoInput 메서드를 실행하라 (자식으로부터 넘어온 이벤트는 케밥 케이스로 작성되어야 함) -->
    <TodoInput @todo-input="todoInput" />
    <TodoList />
   
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
          completed : false
        }
        this.todoList.push(item);
        console.log(JSON.stringify(this.todoList));
      }
    }
  }
</script>
