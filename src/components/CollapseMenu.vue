<template lang="pug">
  div#aside
    el-switch(v-model="isCollapse")
    el-menu(
      default-active="2"
      class="el-menu-vertical"
      @open="handleOpen"
      @close="handleClose"
      :collapse="isCollapse"
    )
      el-submenu(index="1")
        template(slot="title")
          i(class="el-icon-location")
          span(slot="title") One
        el-menu-item-group
          span(slot="title") Group 01
          el-menu-item(index="1-1") 01 - 1
          el-menu-item(index="1-2") 01 - 2
        el-menu-item-group(title="Group Two")
          el-menu-item(index="1-3") 01 - 3
        el-submenu(index="1-4")
          span(slot="title") 01 - 4
          el-menu-item(index="1-4-1") 01 - 4 - 1
      el-menu-item(index="2")
        i(class="el-icon-menu")
        span(slot="title") Two
      el-menu-item(index="3" disable)
        i(class="el-icon-document")
        span(slot="title") Three
      el-menu-item(index="4")
        i(class="el-icon-setting")
        span(slot="title") Four
</template>

<style>
.el-menu-vertical:not(.el-menu--collapse) {
  width: 200px;
  min-height: 400px;
}
</style>

<script>
export default {
  data() {
    return {
      isCollapse: true
    };
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  }
};
</script>
