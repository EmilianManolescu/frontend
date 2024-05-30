<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: {
    TodoList
  }
};
</script>

<style>

body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 0;
  padding: 20px;
  background-color: #f5f5f5;
}
#app {
  max-width: 800px;
  margin: 0 auto;
}
h1 {
  color: #42b983;
}
input {
  padding: 10px;
  margin: 5px;
}
button {
  padding: 10px;
  margin: 5px;
  background-color: #42b983;
  color: white;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: #359d73;
}
</style>
