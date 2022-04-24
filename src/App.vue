<template>
  <div id="app">
    <SwipeCard />
  </div>
</template>

<script>
import SwipeCard from './components/SwipeCard.vue';

export default {
  name: 'App',
  components: {
    SwipeCard,
  },
};
</script>

<style lang="scss">
html,
body {
  height: 100%;
}

#app {
  position: relative;
  overflow: hidden;
  height: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
