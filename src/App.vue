<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
    <NavbarHeader site="AmaVue"></NavbarHeader>
    <Catalog msg="Check those awesome products below!"/>
  </div>
</template>

<script>
import Catalog from './components/Catalog.vue'
import NavbarHeader from "@/components/NavbarHeader";

export default {
  name: 'App',
  components: {
    Catalog,
    NavbarHeader
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
