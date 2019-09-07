<template>
  <div class="scoreboard">
    <span class="text">{{ turnCount }}</span> <span v-for="turn in score" :class="`turn turn--${turn}`" />
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

  computed: {
    matchCount() {
      return this.score.filter(turn => turn === 'match').length;
    },
    turnCount() {
      return this.score.length;
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
.text {
  color: black;
  display: inline-block;
  font: bold 12px / 1.4 arial;
  margin-right: 20px;
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
  border: 2px solid #dddddd;
  background-color: white;
}

.turn--match {
  background: blue;
}
</style>
