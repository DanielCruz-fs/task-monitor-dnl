<template>
      <li class="collection-item">
        <div class="card-panel hoverable">
          <p>
            <label>
              <input type="checkbox" @change="markComplete()" :checked="item.completed"/>
              <span :class="{'is-complete':item.completed}">{{ item.title }}</span>
            </label>


          <a id="delete-btn" class="btn-floating btn-large waves-effect waves-light red secondary-content btn-small" @click="itemDone()">
            <i class="material-icons">delete</i>
          </a>
          <a class="btn-floating btn-large waves-effect waves-light red secondary-content teal lighten-2 btn-small"
             @click="itemUpdate()">
            <i class="material-icons">edit</i>
          </a>
          </p>

        </div>
      </li>
</template>

<script>
  export default {
    name: 'TodoItem',
    props: ['item'],
    methods: {
      markComplete() {
        this.item.completed = !this.item.completed;
      },
      itemDone() {
        this.$root.$emit('markAsCompleted', this.item.id);
      },
      itemUpdate() {
        this.$root.$emit('itemForUpdate', this.item);
      }
    }
  }
</script>

<style scoped>
.is-complete {
  text-decoration: line-through !important;
}
#delete-btn {
  margin-left: 3px;
}
</style>