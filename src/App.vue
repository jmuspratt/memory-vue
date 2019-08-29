<template>
  <div id="app">
    <div class="cards">

       <Card 
        v-for="card in theCards" 
        :key="card.id"
        :card="card" 
        @tapped="cardTapped"
        /> 

    </div>
  </div>
</template>

<script>
 /* eslint-disable */
import Card from "./components/Card.vue";

const animals = ["elephant", "lion", "fox", "tiger", "rabbit", "owl"];
  console.log('animals', animals);

let cards = [];

animals.forEach((animal, index) => {

    const animalCard = {
    id: `${animal}-a`,
    name: animal,
    type: animal,
    image: animal,
    answered: false,
    // flipCount: 0,
  };

  // first copy 
  const cardA = animalCard; 
  cards.push(cardA);
  // second copy
  const cardB = {...animalCard};
  cardB.id = `${animal}-b`;
  cards.push(cardB);
});

  console.log('cards', cards);


// this.shuffle(cards);

export default {
  name: "app",
  components: {
    Card
  },
  data() {
    return {
      flippedCard: null,
      totalFlips: 0,
      // theCards: this.shuffle(cards),
      theCards: cards,

    }
  },

  methods: {
    shuffle(a) {
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    },
    cardTapped(tappedCardID) {
      console.log('card tapped', tappedCardID);
    },
  }
};

</script>

<style lang="scss">
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
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
  // width: 100vw;
  height: 100vh;
}
</style>
