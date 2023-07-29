<script setup>
import TodoCreater from '../components/TodoCreater.vue'
import { ref, watch, computed } from 'vue'
import TodoItems from '../components/TodoItems.vue'

const todoList = ref([])
watch(
  todoList,
  () => {
    setTodoList()
  },
  {
    deep: true
  }
)

const todoCompleted = computed(() => {
  return todoList.value.filter((todo) => todo.isCompleted)
})

const getTodoList = () => {
  const todoListData = localStorage.getItem('todoList')
  if (todoListData) {
    todoList.value = JSON.parse(todoListData)
  }
}
getTodoList()
const setTodoList = () => {
  localStorage.setItem('todoList', JSON.stringify(todoList.value))
}

const createToDo = (todo) => {
  todoList.value.push({
    id: todoList.value.length + 1,
    todo,
    isCompleted: false,
    isEditing: false
  })
}

const ToggleFunction = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted
}

const EditFunction = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing
}

const UpdateFunction = (todoPos, value) => {
  todoList.value[todoPos].todo = value
}
const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId)
}
</script>
<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreater @create-todo="createToDo" />
    <ul class="todo-list">
      <TodoItems
        v-for="(todo, index) in todoList"
        :key="todo.id"
        :todo="todo"
        :index="index"
        @toggle-todo="ToggleFunction"
        @edit-todo="EditFunction"
        @update-todo="UpdateFunction"
        @delete-todo="deleteTodo"
      />
    </ul>
    <div class="todos-msg" v-if="todoCompleted && todoList.length > 0">
      <p>You have completed</p>
    </div>
  </main>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
