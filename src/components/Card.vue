<template>
  <div
    ref="card"
    :class="cardClasses"
    @click="tap"
    :style="cardTransform"
  >
    <div
      class="card__inner2"
    >
      <div
        class="card__inner"
      >
        <div class="card__front" />
        <div
          :data-matchkey="card.matchKey"
          class="card__back"
        >
          <img :src="`${card.imgUrl}`" class="card__img">
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import { TweenMax, Power2 } from 'gsap';

export default {
  name: 'Card',
  props: {
    card: {
      type: Object,
      default: () => {},
    },
    cardTransform: {
      type: String,
      default: () => '',
    },

  },

  data() {
    return {
      orientation: {
        alpha: 4,
        beta: 0,
        gamma: 0,
      },
    };
  },

  computed: {

    cardClasses() {
      return  {
        'card': true,
        'card--flipped': this.card.flipped,
        'card--matched': this.card.matched,
      };
    },
  },

  mounted() {

    const randomAngle1 = Math.floor( Math.random() * 60 );
    const randomAngle2 = Math.floor( Math.random() * 60 );

    TweenMax.to('.card__inner2', 4.5, {
      repeat: -1,
      yoyo: true,
      rotationX: 50,
      rotationY: -40,
      ease: Power2.easeInOut,
    });
  },

  methods: {

    tap() {
      // eslint-disable-next-line
      this.$emit('tapped', this.card.id);
    },
    randomFromRange(min, max) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    },
  },
};
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}

.text {
  color: orange;
}
.card {
  width: auto;
  max-width: 100%;
  display: block;
  perspective: 1000px;
  // overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}

.card__inner2 {
  transform-style: preserve-3d;
  position: relative;
}

// what gets lipped by CSS
.card__inner {
  transition: 0.6s;
  transform-style: preserve-3d;
  position: relative;
}

.card--flipped .card__inner {
  transform: rotateY(180deg);
}

.card--matched .card__inner {
  opacity: 0.2;
}

.card__inner,
.card__inner2,

.card__front,
.card__back {
  border-radius: 5px;
  width: 100%;
  height: 100%;
}

.card__back {
  align-items: center;
  display: flex;
  justify-content: center;
}

.card__img {
  display: block;
  height: auto;
  max-width: 100%;
  max-height: 100%;
}

.card * {
  pointer-events: none;
}

.card__front,
.card__back {
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  position: absolute;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: 50% 50%;
  background-color: #fff;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.card__front {
  background: linear-gradient(45deg, #222, rgb(0, 60, 100));
  z-index: 2;
}

.card__back {
  transform: rotateY(180deg);
}

</style>
