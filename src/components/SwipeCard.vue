<template>
  <div class="swipe-card" :style="{ top: getInitialTopPosition }">
    <div
      ref="swipeCard"
      class="swipe-card-inner-wrapper"
      @touchstart="handleTouchStart"
    >
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: 'SwipeCard',
  props: {
    initialVisibleValue: {
      type: Number,
      required: true,
    },
    minVisibleValue: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      initialTouchStartPosition: 0,
      touchStartPosition: 0,
      touchCurrentPosition: 0,
      minBottomPosition: this.initialVisibleValue - this.minVisibleValue,
    };
  },
  computed: {
    card() {
      return this.$refs.swipeCard;
    },
    getInitialTopPosition() {
      return `calc(100% - ${this.initialVisibleValue}px)`;
    },
    getMaxTopPosition() {
      return -Math.abs(this.card.offsetHeight - this.initialVisibleValue);
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
      if (this.touchCurrentPosition >= this.minBottomPosition) {
        this.touchCurrentPosition = this.minBottomPosition;
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
