<template lang="pug">
  div#app
    el-container
      CollapseMenu
      el-container
        el-header
          h1 header
        el-main
          router-view
</template>

<script>
import CollapseMenu from './components/CollapseMenu';

export default {
  name: 'app',
  components: {
    CollapseMenu
  }
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
