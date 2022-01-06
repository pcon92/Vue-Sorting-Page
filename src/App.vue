<template>
  <bubble-sort
    v-bind:numbersProp="[4, 2, 6, 8, 2, 9, 1, 2]"></bubble-sort>
</template>

<script>
import BubbleSort from './components/BubbleSort.vue';

export default {
  name: 'App',
  components: {
    BubbleSort,
  },
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
  width: 500px;
}
</style>
