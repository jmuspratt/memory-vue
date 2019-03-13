<template>
  <a class="card" :class="{'card--up': faceUp }">
    <div class="card__inner">
      <div class="card__front"></div>

      <div class="card__back">
        <img :src="url">
      </div>
    </div>
  </a>
</template>

<script>
export default {
  name: "Card",
  props: {
    file: String,
    faceUp: Boolean
  },

  data() {
    return {
      url: "/" + this.file + ".png"
    };
  },
  methods: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
* {
  box-sizing: border-box;
}
.card {
  display: block;
  border: 1px solid #ddd;
  border-radius: 15px;
  perspective: 1000px;
}

.card.card--up .card__inner {
  transform: rotateY(180deg);
}

.card__inner,
.card__front,
.card__back {
  // min-height: 300px;
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
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.card__front {
  background: darkGray;
  z-index: 2;
}

.card__back {
  transform: rotateY(180deg);
}

img {
  display: block;
  max-width: 100%;
}
</style>
