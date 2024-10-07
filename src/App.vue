<template>
  <div class="container mt-5">
    <h1 class="text-center mb-4">Vue Todo App</h1>
    <todo-list />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  components: {
    TodoList
  }
}
</script>

<style>

</style>
