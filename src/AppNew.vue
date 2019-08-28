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
