<template>
  <div id="app">
    <app-header :displayTitle="title"/>
    <index class="content"/>
    <tab-bar :menus="menus" @menuClick="handleMenuClick"/>
  </div>
</template>

<script>
import AppHeader from './components/Header'
import TabBar from './components/TabBar'
import tabBar from './model/tabBar'
import Index from './components/Index'

export default {
  name: 'App',
  data () {
    return {
      menus: tabBar.menus,
      title: '本地'
    }
  },
  components: {
    Index,
    AppHeader,
    TabBar
  },
  methods: {
    handleMenuClick (menu) {
      this.$router.push({name: menu.name})
      this.title = menu.text
    }
  }
}
</script>

<style lang="less">
  html, body {
    margin: 0;
    padding: 0;
    background-color: #F5F5F9;
  }

  #app > .content {
    margin-top: 50px;
  }
</style>
