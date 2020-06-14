<template>
  <div id="app" class="container">
    <div id="image-vue">
    <img alt="Vue logo" src="./assets/logo.png">
    </div>
    <app-addtodos @addTodo="createTodo($event)"></app-addtodos>
    <app-todos :todos="todos"></app-todos>
  </div>
</template>

<script>
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';

export default {
  name: 'App',
  components: {
    'app-todos': Todos,
    'app-addtodos': AddTodo
  },
  data() {
    return {
      todos: [
        { id: 1, title: 'todo one', completed: false },
        { id: 2, title: 'todo two', completed: true },
        { id: 3, title: 'todo three', completed: false }
      ]
    }
  },
  mounted() {
    this.$root.$on('markAsCompleted', (data) => {
      console.log('data coming from super child', data);
      this.deleteToDo(data);
    });
  },
  methods: {
    deleteToDo(id) {
      this.todos.splice(this.todos.findIndex(el => el.id == id), 1);
    },
    createTodo(newTodo) {
      console.log(newTodo);
      this.todos.push(newTodo);
    }
  }
}
</script>

<style scoped>
#image-vue {
  text-align: center;
}
</style>
