<template>
<div class="row">
    <form class="col s12" @submit="addToDo($event)">
      <div class="row">
        <div class="input-field col s6 offset-s3">
          <i class="material-icons prefix">{{ updateMode ? 'update' : 'mode_edit' }}</i>
          <textarea ref="mainInput" id="icon_prefix2" class="materialize-textarea" v-model="title"></textarea>
          <label for="icon_prefix2">{{ updateMode ? 'Update Todo' : 'Add Todo' }}</label>
        </div>
      </div>
      <p class="center-align">

      <button class="btn waves-effect waves-light btn-small" type="submit" name="action">
        {{ updateMode ? 'Update' : 'Add' }}
      </button>
      </p>
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';

  export default {
    name: 'AddTodo',
    data() {
      return {
        title: '',
        updateMode: false,
        todoItemShell: {}
      }
    },
    methods: {
      addToDo(e) {
        e.preventDefault();
        if (!this.updateMode) {
          this.todoItemShell = {
            id: uuidv4(),
            title: this.title,
            completed: false
          };
          this.$emit('addTodo', this.todoItemShell);
        } else {
          this.todoItemShell.title = this.title;
          console.log(this.todoItemShell);
          this.updateMode = false;
        }
        this.title = null;
      }
    },
    mounted() {
      this.$root.$on('itemForUpdate', (data) => {
        console.log('data coming for update', data);
        this.updateMode = true;
        this.title = data.title;
        this.todoItemShell = data;
        this.$refs.mainInput.focus();
      });
    }
  }
</script>

<style lang="scss" scoped>

</style>