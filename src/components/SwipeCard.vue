<template>
  <div class="swipe-card" :style="{ top: getInitialTopPosition }">
    <div
      ref="card"
      class="swipe-card-inner-wrapper"
      @touchstart="handleTouchStart"
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
    </div>
  </div>
</template>

<script>
export default {
  name: 'SwipeCard',
  data() {
    return {
      initialTouchStartPosition: 0,
      touchStartPosition: 0,
      touchCurrentPosition: 0,
      initialPxValueOfVisibleCardPart: 250,
      minPxValueOfVisibleCardPart: 100,
    };
  },
  computed: {
    card() {
      return this.$refs.card;
    },
    getInitialTopPosition() {
      return `calc(100% - ${this.initialPxValueOfVisibleCardPart}px)`;
    },
    getMaxTopPosition() {
      return -Math.abs(this.card.offsetHeight - this.initialPxValueOfVisibleCardPart);
    },
    getMinBottomPosition() {
      return Math.abs(
        window.innerHeight
          - this.card.offsetHeight
          - this.initialPxValueOfVisibleCardPart,
      );
    },
  },
  mounted() {
    this.card.addEventListener('touchmove', this.handleTouchMove, false);
  },
  methods: {
    handleTouchStart(e) {
      this.initialTouchStartPosition = e.touches[0].clientY;
      this.touchStartPosition = e.touches[0].clientY - this.touchCurrentPosition;
    },
    handleTouchMove(e) {
      this.touchCurrentPosition = e.changedTouches[0].clientY - this.touchStartPosition;

      // limit up swipe
      if (this.touchCurrentPosition <= this.getMaxTopPosition) {
        this.touchCurrentPosition = this.getMaxTopPosition;
      }
      // limit down swipe
      if (this.touchCurrentPosition >= this.getMinBottomPosition) {
        this.touchCurrentPosition = this.getMinBottomPosition;
      }

      this.card.style.transform = `translateY(${this.touchCurrentPosition}px)`;
    },
  },
};
</script>

<style scoped lang="scss">
.swipe-card {
  position: absolute;
  width: 100%;

  .swipe-card-inner-wrapper {
    position: absolute;
    top: 0;
    max-width: 100%;
    padding: 24px;
    border: 1px solid #000;
    touch-action: none;
  }
}
</style>
