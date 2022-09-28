<template>
  <div id="app">
    <calculator/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'
export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
  body {
    background: #fd7e14 !important;
  }
</style>
