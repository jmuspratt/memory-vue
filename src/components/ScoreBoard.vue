<template>
  <div class="scoreboard">
    <span v-for="turn in score" :class="`turn turn--${turn}`" />
  </div>
</template>

<script>

export default {
  name: 'ScoreBoard',
  props: {
    score: {
      type: Array,
      default: () => null,
    },
  },

};
</script>

<style lang="scss" scoped>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.scoreboard {
  min-height: 40px;
}

.turn {
  height: 10px;
  border-radius: 5px;
  display: inline-block;
  margin-right: 3px;
  width: 10px;
}

.turn--miss {
  background-color: rgb(250, 181, 53);
}

.turn--match {
  background: rgb(70, 208, 243);
}
</style>
