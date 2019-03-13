<template>
  <div id="app">
    <div class="cards">
      <Card :file="animal" v-for="animal in animals"/>
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";

const animals = ["elephant", "lion", "fox", "tiger", "rabbit", "owl"];

function shuffle(a) {
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

const dups = animals.concat(animals);
const dupsShuffled = shuffle(dups);

export default {
  name: "app",
  components: {
    Card
  },
  data() {
    return {
      animals: dupsShuffled
    };
  }
};
</script>

<style lang="scss" scoped>
body {
  padding: 0;
  margin: 0;
}
#app {
  background: #eee;
  margin: 0;
  padding: 40px;
}
.cards {
  list-style: none;
  margin: 0;
  padding: 0;
  display: grid;
  grid-gap: 20px;
  grid-template-columns: 1fr 1fr 1fr 1fr;
}
</style>
