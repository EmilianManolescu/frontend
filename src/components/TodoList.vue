<template>
  <div>
    <h1>Todo List</h1>
    <AddTodo @add-todo="addTodo" />
    <ul>
      <TodoItem 
        v-for="todo in todos" 
        :key="todo.id" 
        :todo="todo" 
        @delete-todo="deleteTodo" 
        @update-todo="updateTodo" 
      />
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import AddTodo from './AddTodo.vue';
import TodoItem from './TodoItem.vue';

export default {
  components: {
    AddTodo,
    TodoItem
  },
  data() {
    return {
      todos: []
    };
  },
  created() {
    this.loadTodos();
  },
  methods: {
    async loadTodos() {
      try {
        const response = await axios.get('http://localhost:3000/api/todos');
        this.todos = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    async addTodo(todo) {
      try {
        const response = await axios.post('http://localhost:3000/api/todos', todo);
        this.todos.push(response.data);
      } catch (error) {
        console.error(error);
      }
    },
    async deleteTodo(id) {
      try {
        await axios.delete(`http://localhost:3000/api/todos/${id}`);
        this.todos = this.todos.filter(todo => todo.id !== id);
      } catch (error) {
        console.error(error);
      }
    },
    async updateTodo(updatedTodo) {
      try {
        const response = await axios.put(`http://localhost:3000/api/todos/${updatedTodo.id}`, updatedTodo);
        const updatedTodoFromServer = response.data;
        const index = this.todos.findIndex(todo => todo.id === updatedTodoFromServer.id);
        if (index !== -1) {
          this.todos.splice(index, 1, updatedTodoFromServer);
        }
      } catch (error) {
        console.error(error);
    }
  }
}
};
</script>

  