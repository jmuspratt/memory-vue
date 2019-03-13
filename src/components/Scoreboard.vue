<template>
  <dl class="scoreboard">
    <dd>Attemps</dd>
    <dt>{{ attemps }}</dt>
    <dd>Matches</dd>
    <dt>{{ matches }}</dt>
  </dl>
</template>

<script>
export default {
  name: "Scoreboard",
  computed: {
    attemps() {
      return 4;
    },
    matches() {
      return 4;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
* {
  box-sizing: border-box;
}
.scoreboard {
  display: block;
  background: black;
  color: white;
}
</style>
