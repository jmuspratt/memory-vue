<template>
  <div id="app">
    <div class="cards">

<!-- <p  -->
<!-- v-for="animal in theCards">{{animal.name}}</p> -->
       <Card 
        v-for="animal in theCards" 
        :key="animal.id"
        :id="animal.id" 
        :animal="animal" 
        @card-flipped="cardFlipped" /> 

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
    id: `${animal}-${index}`,
    name: animal,
    type: animal,
    image: animal,
    answered: false,
    // flipCount: 0,
  };

// Do this twice.
  cards.push(animalCard);
  animalCard.id = `${animal}-${index + 1}`;
  cards.push(animalCard);
});

  // console.log('cards', cards);

// function shuffle(a) {
//   for (let i = a.length - 1; i > 0; i--) {
//     const j = Math.floor(Math.random() * (i + 1));
//     [a[i], a[j]] = [a[j], a[i]];
//   }
//   return a;
// }

// const dups = animals.concat(animals);
// const dupsShuffled = shuffle(dups);

export default {
  name: "app",
  components: {
    Card
  },
  data() {
    return {
      flippedCard: null,
      totalFlips: 0,
      theCards: cards,
    }
  },

// methods: {
//   cardFlipped(card) {
//     if (!flippedCard) {
//       this.flippedCard = card;
//       this.clickedCard = null;
//       return;
//     }
//     if (flippedCard && !clickedCard) {
//       this.clickedCard = card; 
//     }


//     if (this.flippedCard.type === this.clickedCard.type) {
//       this.flippedCard = null;
//       this.clickedCard = null;
//       this.totalFlips++;
//       this.cards.forEach((animal) => {
//         if (animal.type === card.type) {
//           animal.answered = true;
//         }
//       })
//     } else {
//       this.flippedCard = null;
//       this.clickedCard = null;
//       this.totalFlips++;
//     }
//   }
// }
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
