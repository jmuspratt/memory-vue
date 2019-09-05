<template>
  <div :class="cardClasses" @click="tap">
    <div class="card__inner">
      <div class="card__front">
        {{ card.id }}
      </div>
      <div :style="`background-image: url(${imgUrl})`" class="card__back" />
    </div>
  </div>
</template>

<script>

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
      imgUrl: `/${ this.card.image  }.png`,
    };
  },
  computed: {
    cardClasses() {
      return  {
        'card': true,
        'card--flipped': this.card.flipped,
      };
    },
  },
  methods: {
    tap() {
      // eslint-disable-next-line
      console.log('tapped', this.card.id);
      this.$emit('tapped', this.card.id);
    },
  },
};
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}
.card {
  max-width: 100%;
  display: block;
  background-color: #efefef;
  perspective: 1000px;
  // overflow: hidden;
}

.card--flipped .card__inner {
  transform: rotateY(180deg);
}


.card__inner,
.card__front,
.card__back {
  border-radius: 15px;
  min-height: 200px;
}

.card * {
  pointer-events: none;
}

.card__inner {
  transition: 0.6s;
  transform-style: preserve-3d;
  position: relative;
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
  background: royalblue;
  z-index: 2;
}

.card__back {
  transform: rotateY(180deg);
}

</style>
