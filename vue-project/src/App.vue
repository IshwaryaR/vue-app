<script setup lang="ts">
import { RouterView } from 'vue-router'
import TodoHeader from './components/TodoHeader.vue'
import AboutView from './views/AboutView.vue';
</script>

<template>
  <TodoHeader />
  <RouterView />
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,500;0,600;1,500;1,700&display=swap');
* {
  font-family: "Rubik", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
}
</style>
