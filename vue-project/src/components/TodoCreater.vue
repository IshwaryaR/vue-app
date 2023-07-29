<script setup>
import { ref, defineEmits, reactive } from 'vue'
import TodoButton from './TodoButton.vue'

// const todo = ref("");
const todoState = reactive({
  todo: '',
  errorMsg: '',
  invalid: false
})
const emit = defineEmits(['create-todo'])
const createToDo = () => {
  // emit('create-todo', todo.value)
  // console.log(todo.value)
  todoState.invalid = false
  if (todoState.todo !== '') {
    emit('create-todo', todoState.todo)
    todoState.todo = ''
    return
  }
  todoState.errorMsg = 'Please enter a todo'
  todoState.invalid = true
}
</script>

<template>
  <div class="input-wrap" :class="{ 'input-err': todoState.invalid }">
    <input type="text" v-model="todoState.todo" />
    <!--  <button @click="createToDo()">Create</button> -->
    <TodoButton @click="createToDo()">Create</TodoButton>
  </div>
  <p v-if="todoState.invalid">{{ todoState.errorMsg }}</p>
</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &.input-err {
    border-color: red;
  }

  &:focus-within {
    box-shadow:
      0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }

  .err-msg {
    margin-top: 6px;
    font-size: 12px;
    text-align: center;
    color: red;
  }
}
</style>
