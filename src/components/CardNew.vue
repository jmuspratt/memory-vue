const animals = ['fox', 'dog', 'cat'];

const cards = [];

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

// APP
<Card v-for="animal in cards" :flipped-card="flippedCard" :clicked-card="clickedCard" :id="animal.id" :animal="animal" @card-flipped="cardFlipped" />

data() {
  return {
    flippedCard: null,
    totalFlips: 0
  }
},

methods: {
  cardFlipped(card) {
    if (!flippedCard) {
      this.flippedCard = card;
      this.clickedCard = null;
      return;
    }
    if (flippedCard && !clickedCard) {
      this.clickedCard = card; 
    }


    if (this.flippedCard.type === this.clickedCard.type) {
      this.flippedCard = null;
      this.clickedCard = null;
      this.totalFlips++;
      this.cards.forEach((animal) => {
        if (animal.type === card.type) {
          animal.answered = true;
        }
      })
    } else {
      this.flippedCard = null;
      this.clickedCard = null;
      this.totalFlips++;
    }
  },
},