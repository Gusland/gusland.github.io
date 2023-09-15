<template>
  <div id="app">
    <Checkbox />
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
#app {
  font-family: 'Gotham Pro', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
