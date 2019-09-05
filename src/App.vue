<template>
  <div id="app">
    <p>
      {{ flippedCount }}
    </p><div class="cards">
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
import Card from './components/Card.vue';

const animals = ['elephant', 'lion', 'fox', 'tiger', 'rabbit', 'owl'];

const cards = [];

animals.forEach(animal => {

  const animalCard = {
    id: `${animal}-a`,
    name: animal,
    flipped: false,
    type: animal,
    image: animal,
    answered: false,
    // flipCount: 0,
  };

  // first copy
  const cardA = animalCard;
  cards.push(cardA);
  // second copy
  const cardB = { ...animalCard };
  cardB.id = `${animal}-b`;
  cards.push(cardB);
});



// this.shuffle(cards);

export default {
  name: 'App',
  components: {
    Card,
  },
  data() {
    return {
      flippedCard: [],
      totalFlips: 0,
      // theCards: this.shuffle(cards),
      theCards: cards,
    };
  },
  computed: {
    flippedCount() {
      let count = 0;
      this.theCards.forEach(obj => {
        if (obj.flipped) {
          count++;
        }
      });
      return count;
    },
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
      // eslint-disable-next-line
      console.log('card tapped', tappedCardID);
      this.handleTap(tappedCardID);
    },

    handleTap(cardID) {
      // eslint-disable-next-line
      console.log('handling tap on ', cardID);
      // find it
      // const tappedCard = this.theCards.find(obj => obj.id === cardID);
      const newCards = this.theCards.map(card => card.id === cardID ? { ...card, flipped: !card.flipped } : card );
      // update cards
      this.theCards = newCards;
    },
  },
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
