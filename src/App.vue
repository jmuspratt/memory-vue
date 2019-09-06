<template>
  <div id="app">
    <p>
      turnCount: {{ turnCount }}
    </p>
    <p>
      flips this turn: {{ flipsThisTurn }}
    </p>
    <p>
      flipped count: {{ flippedCount }}
    </p>
    <p>
      match count: {{ matchCount }}
    </p>
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
import Card from './components/Card.vue';

const animals = ['elephant', 'lion', 'fox', 'tiger', 'rabbit', 'owl'];

const cards = [];

animals.forEach(animal => {

  const animalCard = {
    id: `${animal}-a`,
    name: animal,
    matchKey: animal,
    flipped: false,
    type: animal,
    image: animal,
    answered: false,
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
      totalFlips: 0,
      // theCards: this.shuffle(cards),
      theCards: cards,
      flipsThisTurn: 0,
      turnCount: 0,
      firstFlipID: null,
      firstFlipMatchKey: null,
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
    matchCount() {
      switch (this.flipsThisTurn) {
        case 1:
          return (this.flippedCount - 1) / 2;
        case 2:
          return this.flippedCount / 2;
        default:
          return this.flippedCount / 2 ;
      }
    },
  },
  methods: {
    incrementFlipsThisTurn() {
      console.error('incrementing');

      this.flipsThisTurn ++;
    },
    shuffle(a) {
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    },

    cardTapped(cardID) {
      // eslint-disable-next-line
      console.error('handling tap on ', cardID);
      // find it a
      const tappedCard = this.theCards.find(obj => obj.id === cardID);
      console.error('tapped card is ', tappedCard.name);

      if (tappedCard.flipped) {
        console.error(tappedCard.name, ' is already flipped ');
        return;
      }


      this.incrementFlipsThisTurn();

      if (this.flipsThisTurn === 1) {
        console.error('first turn ');
        // store ID
        this.firstFlipID = cardID;
        this.firstFlipMatchKey = tappedCard.matchKey;

        console.error('first card MATCH KEY IS', this.firstFlipMatchKey);
        // flip the card
        this.flipCard(cardID);

      }
      if (this.flipsThisTurn === 2) {
        console.error('second turn ');
        this.flipCard(cardID);

        // check match
        if (tappedCard.matchKey === this.firstFlipMatchKey) {
          console.error('match!');

          setTimeout(() => {
            this.flipsThisTurn = 0;
            this.turnCount ++;
          }, 1000);
        } else {
          // not a match
          setTimeout(() => {
            // Unflip this and the first
            this.flipCard(cardID);
            this.flipCard(this.firstFlipID);
            this.flipsThisTurn = 0;
            this.turnCount ++;
          }, 1000);
        }
      }
    },
    flipCard(cardID) {
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
