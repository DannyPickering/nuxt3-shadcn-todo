<script setup lang="ts">
  import { ref, computed } from 'vue'
  import { v4 as uuidv4 } from 'uuid';
  import type { Todo } from '@/types';

  onMounted(() => {
    const storedTodos = localStorage.getItem('todos')
    if (storedTodos !== null) {
      todos.value = JSON.parse(storedTodos) || []
    }
  })

  let todos = ref<Todo[]>([])

  const filter = ref<string>('none')

  const filteredTodos = computed(() => {
    // TODO create filters
    return filter.value === 'none' ?  todos.value : todos.value
    
  })

  const activeTodos = computed(() => todos.value.filter((todo) => !todo.completed))

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

  const completeAll = () => {
    if (activeTodos.value.length === 0) {
      todos.value.forEach((todo) => todo.completed = false)
    } else {
      todos.value.forEach((todo) => todo.completed = true)
    }
  }

  const updateLocalStorage = () => {
    localStorage.setItem('todos', JSON.stringify(todos.value))
  }


</script>

<template>
  <div class="mx-auto max-w-[80ch]">
    <div>
      <TodoHeader :todos="filteredTodos" @addTodo="addTodo" @completeAll="completeAll"/>
    </div>

    <div v-if="todos.length < 1" class="bg-neutral-50 rounded-b-xl shadow-2xl px-2 py-8 text-center text-xl text-slate-600">
      <p>Nothing todo! Add some tasks above.</p>
    </div>
    <div v-else>
      <ul class="bg-neutral-50 rounded-b-xl shadow-2xl">
        <TodoItem v-for="(todo, index) in filteredTodos" :key="index" :todo="todo" @toggleCompleted="toggleCompleted"/>
      </ul>
    </div>
  </div>
</template>