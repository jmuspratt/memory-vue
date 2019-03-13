<template>
  <div id="app">
    <Scoreboard/>

    <div class="cards">
      <Card
        v-for="(animal, index) in theAnimals"
        :key="index"
        :file="animal.name"
        :isFaceUp="animal.isFaceUp"
        @click.native="cardClick"
      />
    </div>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import Scoreboard from "./components/Scoreboard.vue";

const animals = ["elephant", "lion", "fox", "tiger", "rabbit", "owl"];

function shuffle(a) {
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

const animalObjects = [];
animals.forEach(item => {
  animalObjects.push({
    name: item,
    isFaceUp: false
  });
});

console.log(animalObjects);

const dups = animals.concat(animalObjects);
const dupsShuffled = shuffle(dups);

export default {
  name: "app",
  components: {
    Card,
    Scoreboard
  },
  data() {
    return {
      theAnimals: dupsShuffled,
      flipCounter: 0,
      pair: {
        firstCard: null,
        secondCard: null
      }
    };
  },
  methods: {
    cardClick($event) {
      console.log("card click", $event);
      this.theAnimals[4].isFaceUp = true;
      console.log(this.theAnimals);
    }
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

li {
  max-width: 100%;
  display: block;
  cursor: pointer;
  // width: 25%;
  // margin: 10px;
}
.cards__button {
  display: block;
  appearance: none;
  -webkit-appearance: none;
}
</style>
