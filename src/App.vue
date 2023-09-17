<template>
  <div id="app">
    <Checkbox/>
  </div>
</template>

<script>
import Checkbox from './components/Checkbox';

export default {
  name: 'App',
  components: {
    Checkbox,
  },
};
</script>

<style>
:root {
  --white: #fff;
  --primary-200: #92A4C8;
  --primary-300: #3E517A;
  --primary-400: #303F5F;
  --primary-500: #212B41;
  --primary-700: #151B29;
  --primary-900: #0E121B;
  --secondary-500: #4AB4FF;
}

#app {
  font-family: 'Gotham Pro', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}

body {
  background-color: var(--primary-500);
}
</style>
