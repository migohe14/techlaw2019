<template>
  <div id="app">
    <header-component></header-component>
    <router-view/>
  </div>
</template>

<script>
import HeaderComponent from "./components/HeaderComponent";

export default {
  name: 'app',
  components: {
    HeaderComponent
  }
}
</script>

<style>

</style>
