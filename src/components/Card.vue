<template>
  <div class="card" @click="flip">
    <div class="card__inner">
      <div class="card__front"></div>

      <div class="card__back">
        <img :src="url">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    file: String
  },
  data() {
    return {
      url: "/" + this.file + ".png"
    };
  },
  methods: {
    flip($event) {
      $event.target.classList.toggle("flipped");
      this.$emit("flipped");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
* {
  box-sizing: border-box;
}
.card {
  max-width: 100%;
  display: block;
  border: 1px solid #ddd;
  border-radius: 15px;
  perspective: 1000px;
  overflow: hidden;
}

.card.flipped .card__inner {
  transform: rotateY(180deg);
}

.card__inner,
.card__front,
.card__back {
  min-height: 250px;
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
  background: royalblue;
  z-index: 2;
}

.card__back {
  transform: rotateY(180deg);
}

img {
  display: block;
  object-fit: cover;
  object-position: 50% 50%;
}
</style>
