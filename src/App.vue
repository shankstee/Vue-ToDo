<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <todo-list></todo-list>
  </div>
</template>

<script>
import TodoList from "./components/TodoList"

export default {
  name: 'App',
  components: {
    TodoList

  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

.container {
  margin: 0 auto;
  max-width: 700px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
