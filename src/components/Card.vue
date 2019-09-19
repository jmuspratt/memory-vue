<template>
  <div
    ref="card"
    :class="cardClasses"
    @click="tap"
    :style="cardTranslate"
  >
    <svg
      viewBox="0 0 120 120"
    >
      <defs>
        <mask id="mask">
          <rect
            ref="maskRect"
            width="240"
            height="240"
            fill="gray"
          />
          <circle
            ref="maskCircle"
            r="80"
            cx="120"
            cy="120"
            fill="black"
          />
        </mask>
      </defs>
    </svg>
    <div class="card__inner">
      <svg id="" class="card__cover">
        <circle
          ref="circle"
          cx="60"
          cy="60"
          r="120"
          mask="url(#mask)"
        />
      </svg>
      <div
        class="card__content"
      >
        <img :src="`${card.imgUrl}`" class="card__img">
      </div>
    </div>
  </div>
</template>

<script>

import { TweenMax } from 'gsap/all';
// console.log('TCL: TweenMax', TweenMax);

export default {
  name: 'Card',
  props: {
    card: {
      type: Object,
      default: () => {},
    },

  },

  data() {
    return {
      gravity: {
        x: 0,
        y: 0,
      },
      delta: [0, 0],
      pos: {
        x: 0,
        y: 0,
      },
    };
  },
  computed: {

    flipped() {
      return this.card.flipped;
    },

    cardTranslate() {
      return null;
      // return `transform: translate(${this.pos.x}px, ${this.posY}px);`;
    },

    cardClasses() {
      return  {
        'card': true,
        // 'card--flipped': this.card.flipped,
        'card--matched': this.card.matched,
      };
    },
  },

  watch: {
    flipped() {

      const el = this.$refs.maskCircle;
      const newRadius = this.flipped ? 0 : 120;

      TweenMax.to(el, .375, {
        attr: {
          r: newRadius,
        },
      });
    },
  },

  created() {
    window.addEventListener( 'deviceorientation', this.onDeviceTilt, false );

  },
  methods: {
    onDeviceTilt(event) {
      // const rand = this.randomFromRange(30, 50);
      if ( event.beta ) {
        this.gravity.x = Math.sin( event.gamma * Math.PI / 180 );
        this.gravity.y = Math.sin( ( Math.PI / 4 ) + event.beta * Math.PI / 180 );

        this.posX = this.gravity.x * 8 + this.delta[0] ;
        this.posY = this.gravity.y * 8 + this.delta[1] ;

        // update delta with new positions
        this.delta[0] = this.posX;
        this.delta[1] = this.posY;
      }
    },
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

.card {
  --card-size: 240px;
}

.card {
  display: block;
  // perspective: 1000px;
  width: var(--card-size);
  height: var(--card-size);
  position: relative;

}


.card__cover {
  position: absolute;
  width: var(--card-size);
  left: 0;
  height: var(--card-size);
  top: 0;
  z-index: 2;
  circle {
    mask-position: 0% 0%;
    // transform-origin: 50% 50%;
    // transform: translate(120px, 120px);
    fill: blue;
  }
}


.card__content {
  height: (--card-size);
  width: (--card-size);
}

.card__img {
  position: absolute;
  top: 25px;
  left: 25px;
  display: block;
  height: auto;
  max-width: 100%;
}

// .card * {
//   pointer-events: none;
// }

</style>
