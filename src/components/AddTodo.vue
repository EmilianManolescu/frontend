<template>
    <div>
      <input v-model="newTodoText" @keyup.enter="addTodo" placeholder="Add a new todo" />
      <button @click="addTodo">Add</button>
    </div>
</template>
  
<script>
  export default {
    data() {
      return {
        newTodoText: ''
      };
    },
    methods: {
      addTodo() {
        if (this.newTodoText.trim()) {
          const newTodo = {
            id: Date.now(),
            text: this.newTodoText.trim()
          };
          this.$emit('add-todo', newTodo);
          this.newTodoText = '';
        }
      }
    }
  };
</script>
  