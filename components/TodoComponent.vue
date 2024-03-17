<script setup lang="ts">
  import { ref, computed } from 'vue'
  import { v4 as uuidv4 } from 'uuid';
  
  interface Todo {
    completed: boolean;
    title: string,
    id: string
  }

  onMounted(() => {
    const storedTodos = localStorage.getItem('todos')
    if (storedTodos !== null) {
      todos.value = JSON.parse(storedTodos) || []
    }
  })

  let todos = ref<Todo[]>([])

  const filteredTodos = computed(() => {
    // TODO create filters
    return todos.value
  })



  const addTodo = (value: String) => {
    todos.value.push({
      completed: false,
      title: value.trim(),
      id: uuidv4()
    })

    updateLocalStorage()
  }

  const toggleCompleted = (id: string) => {
    const idx = todos.value.findIndex(obj => obj.id === id)

    if (idx !== -1) {
      todos.value[idx]['completed'] = !todos.value[idx]['completed']

      updateLocalStorage()
    }
  }

  const updateLocalStorage = () => {
    localStorage.setItem('todos', JSON.stringify(todos.value))
  }


</script>

<template>
  <div class="mx-auto max-w-[80ch]">
    <div>
      <TodoHeader @addTodo="addTodo"/>
    </div>

    <div v-show="todos.length > 0">
      <ul class="bg-neutral-50 rounded-b-xl shadow-2xl">
        <TodoItem v-for="(todo, index) in todos" :key="index" :todo="todo" @toggleCompleted="toggleCompleted"/>
      </ul>
    </div>
  </div>
</template>