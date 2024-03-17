<script setup lang="ts">
  import { ref } from 'vue'

  import { Label } from '@/components/ui/label'
  import { Checkbox } from '@/components/ui/checkbox'
  import { Input } from '@/components/ui/input'
  import { Button } from '@/components/ui/button'
  import { CornerDownRight } from 'lucide-vue-next'

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
  <div class="flex flex-row gap-3 bg-slate-200 py-5 px-2 rounded-t-xl shadow-2xl">
    <div class="flex flex-col items-center justify-center gap-1 cursor-pointer relative">
      <Label
        for="completeAll"
        class="font-cursive text-2xl font-bold text-center leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70 absolute left-[-90px] top-[-20px] rotate-[-35deg] min-w-[80px] rounded-full"
      >
        <span>Complete all</span>
      </Label>
      <CornerDownRight class="absolute left-[-40px]" />
      <Checkbox id="completeAll" class="min-w-6 min-h-6 rounded-full" />
    </div>
    <Input v-model="todoValue" @keyup.enter="addTodo()" placeholder="What needs to be done?" autofocus/>
    <Button class="min-w-[70px]" @click="addTodo()">+</Button>
  </div>
</template>

<style>
  .curved-label {
    shape-outside: circle();
    clip-path: circle();
  }
</style>