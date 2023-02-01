<template>
  <div class="home">
    <ListOfProduct></ListOfProduct>
  </div>
</template>

<script>
import ListOfProduct from './components/ListOfProduct.vue';

export default {
components:{
  ListOfProduct,
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
  margin-top: 60px;
}
</style>
