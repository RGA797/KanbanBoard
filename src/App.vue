<!-- upper level app. implements kanbanboard-->
<template>
    <KanbanBoard></KanbanBoard>
</template>

<script>
import KanbanBoard from './components/KanbanBoard.vue'

export default {
  name: 'App',
  components: {
    KanbanBoard
  },
}
</script>

<style>
:root {
  --primary-color: #f7d1cd; 
  --secondary-color: #59302D; 
  --button-color: #59302D; 
  --button-text-color: #ffffff; 
  --font-family: 'Helvetica Neue', Arial, sans-serif; 
}
</style>
