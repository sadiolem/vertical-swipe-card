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

      const isUpDirection = (this.initialTouchStartPosition - e.changedTouches[0].clientY) > 0;

      if (isUpDirection) {
        const isFullCardVisible = window.innerHeight
          - this.card.getBoundingClientRect().bottom >= 0;

        if (isFullCardVisible) {
          // limit up swipe
          this.touchCurrentPosition = -Math.abs(
            this.card.getBoundingClientRect().bottom
            - this.card.getBoundingClientRect().top
            - this.initialPxValueOfVisibleCardPart,
          );
        }
      } else {
        const isMinPartOfCardIsVisible = window.innerHeight
          - this.card.getBoundingClientRect().top
          <= this.minPxValueOfVisibleCardPart;

        if (isMinPartOfCardIsVisible) {
          // limit down swipe
          this.touchCurrentPosition = Math.abs(
            window.innerHeight
            - this.card.getBoundingClientRect().top
            - this.initialPxValueOfVisibleCardPart,
          );
        }
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
