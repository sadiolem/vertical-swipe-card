<template>
  <div id="app">
    <SwipeCard
      :initial-visible-value="250"
      :min-visible-value="100"
    >
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit.
        Tempora numquam temporibus accusantium eum! Asperiores, quidem.
        Voluptate harum ducimus delectus officia,
        alias vitae doloribus praesentium ut sapiente officiis ea ad nihil.
      </p>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit.
        Tempora numquam temporibus accusantium eum! Asperiores, quidem.
        Voluptate harum ducimus delectus officia,
        alias vitae doloribus praesentium ut sapiente officiis ea ad nihil.
      </p>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit.
        Tempora numquam temporibus accusantium eum! Asperiores, quidem.
        Voluptate harum ducimus delectus officia,
        alias vitae doloribus praesentium ut sapiente officiis ea ad nihil.
      </p>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit.
        Tempora numquam temporibus accusantium eum! Asperiores, quidem.
        Voluptate harum ducimus delectus officia,
        alias vitae doloribus praesentium ut sapiente officiis ea ad nihil.
      </p>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit.
        Tempora numquam temporibus accusantium eum! Asperiores, quidem.
        Voluptate harum ducimus delectus officia,
        alias vitae doloribus praesentium ut sapiente officiis ea ad nihil.
      </p>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit.
        Tempora numquam temporibus accusantium eum! Asperiores, quidem.
        Voluptate harum ducimus delectus officia,
        alias vitae doloribus praesentium ut sapiente officiis ea ad nihil.
      </p>
    </SwipeCard>
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
