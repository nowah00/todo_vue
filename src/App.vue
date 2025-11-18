<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoList from './components/TodoList.vue';
import TodoInput from './components/TodoInput.vue';
import { computed } from 'vue';

export default {
  components: {
    TodoHeader,
    TodoList,
    TodoInput,
  },

  data() {
    return {
      todo: [],
      current: 'all',
    };
  },

  methods: {
    addTodo(inputMsg) {
      const item = {
        id: Math.random(), // todo id를 고유값으로 랜덤하게 저장
        msg: inputMsg, // 할일 content
        complete: false, // 완료 여부
      };
      this.todo.push(item);
    },

    updateTab(tab) {
      this.current = tab;
    },

    deleteTodo(id) {
      this.todo = this.todo.filter((v) => v.id !== id);
    },
    updateTodo(id) {
      this.todo = this.todo.map((v) =>
        v.id === id ? { ...v, completed: !v.completed } : v
      );
    },
  },

  // list에 필터를 걸어서 보낼지 모두 보낼지 선택하는 메서드
  computed: {
    computedTodo() {
      if (this.current === 'all') {
        return this.todo;
      } else {
        return this.todo.filter((v) => v.completed);
      }
    },
  },
};
</script>

<template>
  <div class="todo">
    <!-- TodoInput으로부터 전달받은 현재의 todo를 TodoHeader에다가 전달 -->
    <TodoHeader :current="current" @update-tab="updateTab" />
    <!-- TodoList 컴포넌트로 computedTodo를 전달 -->
    <TodoList
      :computed-todo="computedTodo"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"
    />
    <TodoInput @add-todo="addTodo" />
  </div>
</template>
