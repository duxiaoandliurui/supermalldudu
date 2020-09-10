<template>
  <div id="app">
    <router-view></router-view>
    <main-tab-bar></main-tab-bar>

  </div>
</template>
<script>
  import MainTabBar from "components/content/mainTabbar/MainTabBar";

  export default {
    name: 'app',
    components: {
      MainTabBar
    }
  }
</script>
<style>
  /*引入资源*/
  @import "./assets/css/base.css";
</style>
