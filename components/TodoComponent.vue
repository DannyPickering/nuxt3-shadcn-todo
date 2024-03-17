<script setup lang="ts">
  import { ref, computed } from 'vue'
  import { v4 as uuidv4 } from 'uuid';

  // import TodoHeader from '@/components/TodoHeader.vue'
  import TodoItem from './TodoItem.vue'
  

  onMounted(() => {
    if (typeof localStorage != undefined) {
      todos.value = JSON.parse(localStorage.getItem('todos')) || []
    }
  })

  let todos = ref([])

  const filteredTodos = computed(() => {
    // TODO create filters
    return todos.value
  })

  function addTodo(value) {
    todos.value.push({
      completed: false,
      title: value,
      id: uuidv4()
    })

    updateLocalStorage()
  }

  function updateLocalStorage () {
    localStorage.setItem('todos', JSON.stringify(todos.value))
  }
</script>

<template>
  <div class="mx-auto max-w-[80ch]">
    <div>
      <TodoHeader @addTodo="addTodo"/>
    </div>

    <div v-show="todos.length > 0">
      <ul>
        <TodoItem v-for="(todo, index) in todos" :key="index" :todo="todo"/>
      </ul>
    </div>
  </div>
</template>