<script>
export default {
  data() {
    return {
      inputMsg: '', // 사용자가 입력한 todo 데이터
    };
  },

  emits: ['addTodo'],

  methods: {
    onEnter(e) {
      // 한글 IME 조합 중이면 무시
      if (e.isComposing || e.keyCode === 229) return;

      this.addTodo();
    },

    addTodo() {
      console.log(this.inputMsg);
      this.$emit('addTodo', this.inputMsg); // 부모 컴포넌트한테 이벤트 호출
      this.inputMsg = '';
    },
  },
};
</script>

<template>
  <div class="todo__input">
    <input
      v-model="inputMsg"
      type="text"
      class="todo__input-text"
      placeholder="할 일을 입력하세요."
      @keydown.enter="onEnter"
    />
    <button class="todo__input-btn" @click="addTodo">등록</button>
  </div>
</template>
