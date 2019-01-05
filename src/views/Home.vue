<template lang="pug">
  div.home
    img(src="../assets/logo.png")
    div
      p
        | If Element is successfully added to this project, you'll see an
        | <code v-text="'<el-button>'"></code>
        | below
      el-button el-button
    HelloWorld(msg="Welcome to Vue.js App")
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';

export default {
  name: 'home',
  components: {
    HelloWorld
  }
};
</script>
