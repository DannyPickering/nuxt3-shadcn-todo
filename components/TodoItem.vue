<script setup lang="ts">
  import { Checkbox } from '@/components/ui/checkbox'
  import { Label } from '@/components/ui/label'

  const props = defineProps({
    todo: {
      type: Object as () => {title: string, completed: boolean, id: string },
      required: true
    }
  })

</script>

<template>
  <li class="py-4 px-2 border-b border-slate-200 last:border-b-0">
    <div class="flex flex-row gap-3 items-center">
      <div class="flex justify-center">
        <Checkbox class="min-w-6 min-h-6 rounded-full" @click="$emit('toggleCompleted', todo.id)" :checked="todo.completed" />
      </div>
      <Label class="pl-2">{{ todo.title }}</Label>
    </div>
  </li>
</template>