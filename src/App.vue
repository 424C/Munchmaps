<template>
  <div id="app">
    <Header />
    <food-card />
  </div>
</template>

<script>
import FoodCard from './components/FoodCard'
import Header from './components/layout/Header'
import '../dist/style.css' 

export default {
  name: 'app',
  components: {
    Header,
    FoodCard,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
</style>
