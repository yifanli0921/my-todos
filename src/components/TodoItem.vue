<template>
  <div class="todo-item">
    <div class="todo-item-left">
      <input type="checkbox" v-model="completed">
      <div v-if="!editing" @dblclick="editTodo"
           class="todo-item-label" v-bind:class = "{completed : completed } ">{{title}}</div>
      <input
        v-else class="todo-item-edit"
        type="text"
        v-model="title"
        @blur="doneEdit"
        @keyup.esc="cancelEdit"
        v-focus
      >
      <div class="remove-item" @click="removeTodo(index)">
        <button class="delete-button">Delete</button>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: 'todo-item',
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  data () {
    return {
      'id': this.todo.id,
      'title': this.todo.title,
      'completed': this.todo.completed,
      'editing': this.todo.editing,
      'beforeEditCache': ''
    }
  },
  methods: {
    removeTodo (index) {
      this.$emit('removedTodo', index)
    }
  }
}
</script>

<style scoped>

</style>
