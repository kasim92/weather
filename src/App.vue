<template>
  <div id="app">
    <Header/>
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Header from './components/header'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Header
  }
}
</script>

<style>
  body{
    background-color: #E5E5E5;
  }


</style>
