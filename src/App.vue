<template>
  <div id="app" class="app">
    <ScoreBoard
      :score="score"
      @reset="reset"
    />
    <div
      class="grid"
    >
      <Card
        v-for="card in theCards"
        :key="card.id"
        :card="card"
        @tapped="cardTapped"
      />
      </scoreboard>
    </div>
  </div>
</template>

<script>
import Card from './components/Card.vue';
import ScoreBoard from './components/ScoreBoard.vue';

// const animals = ['elephant', 'lion', 'fox', 'tiger', 'rabbit', 'owl'];

const shapes = [
  'triangle',
  'star',
  'rhombus',
  'square',
  'pentagon',
  'hexagon',
  'oval',
  'circle'];

const cards = [];

shapes.forEach(item => {


  const card = {
    matchKey: item,
    flipped: false,
    id: `${item}-a`,
    imgUrl: `/images/shapes/${item}.png`,
    matched: false,
  };

  // first copy
  const cardA = card;
  cards.push(cardA);
  // second copy
  const cardB = { ...card };
  cardB.id = `${item}-b`;
  cards.push(cardB);

});

function shuffle(a) {
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

shuffle(cards);

function initState() {
  return {
    totalFlips: 0,
    // theCards: this.shuffle(cards),
    theCards: cards,
    flipsThisTurn: 0,
    turnCount: 0,
    firstFlipID: null,
    firstFlipMatchKey: null,
    score: [],
  };
}

export default {
  name: 'App',
  components: {
    Card,
    ScoreBoard,
  },
  data() {
    return initState();
  },
  computed: {

    matchCount() {
      return this.theCards.filter(card => card.matched === true).length / 2;
    },
  },

  mounted() {
    if (navigator.serviceWorker && !navigator.serviceWorker.controller) { navigator.serviceWorker.register('/serviceworker.js'); }
  },
  methods: {
    incrementFlipsThisTurn() {
      this.flipsThisTurn ++;
    },

    cardTapped(tappedCardID) {
      // store a copy of the card data as tappedCard
      const tappedCard = this.theCards.find(obj => obj.id === tappedCardID);

      if (tappedCard.flipped) {
        return;
      }

      // Increment flip count for this turn
      this.incrementFlipsThisTurn();

      if (this.flipsThisTurn === 1) {
        this.runTurn1(tappedCard);

      }
      if (this.flipsThisTurn === 2) {
        this.runTurn2(tappedCard);
      }
    },

    runTurn1(tappedCard) {
      // flip the card face up
      this.flipCard(tappedCard.id);

      // store ID and Matchkey of first flipped card
      this.firstFlipID = tappedCard.id;
      this.firstFlipMatchKey = tappedCard.matchKey;
    },

    runTurn2(tappedCard) {
      // flip the card face up
      this.flipCard(tappedCard.id);
      this.checkMatch(tappedCard);
    },

    checkMatch(tappedCard) {
      // check match
      setTimeout(() => {
        if (tappedCard.matchKey === this.firstFlipMatchKey) {
          // Match!
          // reset flips counter
          this.flipsThisTurn = 0;
          // update the 2 cards 'matched' prop
          const newCards = this.theCards.map(card => ([tappedCard.id, this.firstFlipID].includes(card.id)) ? { ...card, matched: true } : card );
          this.theCards = newCards;

          // update score
          this.score.push('match');

        } else {
          // Not a match
          // Turn both cards back face down
          this.flipCard(tappedCard.id);
          this.flipCard(this.firstFlipID);
          this.flipsThisTurn = 0;
          // update the score
          this.score.push('miss');
        }
        // increment turn count
        this.turnCount ++;

      }, 1000);
    },


    flipCard(tappedCardID) {
      const newCards = this.theCards.map(card => card.id === tappedCardID ? { ...card, flipped: !card.flipped } : card );
      // update cards
      this.theCards = newCards;
    },
    reset() {
      Object.assign(this.$data, initState());
    },
  },
};

</script>

<style lang="scss">
body {
  background: #222;
  color: #fff;
  padding: 0;
  margin: 0;
  font-family: arial, helvetica, sans-serif;
  font-size: 15px;
}



.app {
  margin: 0;
  padding: 20px;

  @media (min-width: 700px) {
    padding: 50px;
  }
}

.grid {
  list-style: none;
  margin: 0;
  padding: 0;
  display: grid;
  grid-gap: 20px;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  width: calc(100vw -80px);
  height: calc(100vh - 100px);
}

.grid__cell {
  // width: 100%;
  // height: 100%;
}


</style>
