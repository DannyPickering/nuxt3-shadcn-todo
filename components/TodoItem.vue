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
  <li>
    <div>
      <Checkbox id="completed" />
      <Label>{{ todo.title }}</Label>
      <pre>{{ todo }}</pre>
    </div>
  </li>
</template>