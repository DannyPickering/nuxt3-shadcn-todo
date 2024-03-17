<script setup lang="ts">
  import { ref } from 'vue'

  import { Label } from '@/components/ui/label'
  import { Checkbox } from '@/components/ui/checkbox'
  import { Input } from '@/components/ui/input'
  import { Button } from '@/components/ui/button'

  const todoValue = ref('')

  const emits = defineEmits(['addTodo'])
  const addTodo = () => {
    if (todoValue.value.length > 0) {
      emits('addTodo', todoValue.value)
      todoValue.value =''
    }
    // TODO: field validation
  }
</script>

<template>
  <div class="flex flex-row gap-3 bg-slate-200 py-5 px-2 rounded-sm">
    <div class="flex flex-col items-center justify-center gap-1 min-w-[80px] cursor-pointer">
      <Label
        for="completeAll"
        class="text-[0.65rem] text-center leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
      >
        Complete all
      </Label>
      <Checkbox id="completeAll" />
    </div>
    <Input v-model="todoValue" @keyup.enter="addTodo()" placeholder="What needs to be done?" autofocus/>
    <Button class="min-w-[70px]" @click="addTodo()">+</Button>
  </div>
</template>