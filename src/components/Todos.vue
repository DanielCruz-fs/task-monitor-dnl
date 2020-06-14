<template>
  <div>
    <ul class="collection with-header">
      <li class="collection-header"><h4>Todos</h4></li>

      <app-todoitem v-for="todo in todos" :key="todo.id" :item="todo">
      </app-todoitem>

    </ul>
  </div>
</template>

<script>
import TodoItem from './TodoItem';

export default {
  name: 'Todos',
  props: ['todos'],
  components: {
    'app-todoitem': TodoItem 
  }
};
</script>

<style scoped></style>
