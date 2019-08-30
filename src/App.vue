<template>
  <div class="container">
    <div class="mail-box">
      <app-sidebar></app-sidebar>
      <app-content></app-content>
    </div>
  </div>
</template>

<script>
import Sidebar from './components/Sidebar'
import Content from './components/Content'

export default {
  components: {
    appSidebar: Sidebar,
    appContent: Content
  }
};
</script>

<style>
</style>
