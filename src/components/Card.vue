<template>
  <div class="card" @click="flip" >
    <img :src="url" />
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    file: String
  },
  data() {
    return {
      url: '/' + this.file + '.png',
    }
  },
  methods: {
    flip($event) {
      $event.target.classList.toggle('flipped')
      this.$emit('flipped')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>

* {
  box-sizing: border-box;
}
.card {
  border: 1px solid #ddd;
  border-radius: 15px;
   &.flipped {
    border: 1px solid red;
    }
}
  img {
    display: block;
    max-width: 100%;
  
  pointer-events: none;
  }

</style>
