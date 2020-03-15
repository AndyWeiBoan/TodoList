<template>
  <div class="TodoList">
    <TodoList msg="This is Todo list"/>
  </div>
</template>

<script>
// @ is an alias to /src
import TodoList from '@/components/TodoList.vue'

export default {
  name: 'Todo',
  components: {
    TodoList
  }
}
</script>
