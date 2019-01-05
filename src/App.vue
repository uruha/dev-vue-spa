<template lang="pug">
  div#app
    img(src="./assets/logo.png")
    div
      p
        | If Element is successfully added to this project, you'll see an
        | <code v-text="'<el-button>'"></code>
        | below
      el-button el-button
    HelloWorld(msg="Welcome to Your Vue.js App")
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'app',
  components: {
    HelloWorld
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
