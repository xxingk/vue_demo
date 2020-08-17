<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
    <TodoList/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import TodoList from './components/TodoList'

export default {
  name: 'App',
  components: {
    HelloWorld,
    TodoList
  }
}
</script>

<style>

*{
  box-sizing: border-box;
}

.container {
  width: 600px;
  margin: 0 auto;
}

.logo {
  width: 100px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 24px;
}

.container div {
  text-align: left;
}
</style>
