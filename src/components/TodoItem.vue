<template>
    <li>
      <span v-if="!isEditing">{{ todo.text }}</span>
      <input v-else v-model="newText" @keyup.enter="saveEdit" @blur="saveEdit" />
      <button @click="editTodo">Edit</button>
      <button @click="deleteTodo">Delete</button>
    </li>
  </template>
  
<script>
  export default {
    props: {
      todo: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        isEditing: false,
        newText: this.todo.text
      };
    },
    methods: {
      editTodo() {
        this.isEditing = true;
        this.$nextTick(() => this.$el.querySelector('input').focus());
      },
      saveEdit() {
        if (this.newText.trim()) {
          this.$emit('update-todo', { ...this.todo, text: this.newText });
          this.isEditing = false;
        } else {
          this.cancelEdit();
        }
      },
      cancelEdit() {
        this.newText = this.todo.text;
        this.isEditing = false;
      },
      deleteTodo() {
        this.$emit('delete-todo', this.todo.id);
      }
    }
  };
</script>
  