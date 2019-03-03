<template>
  <div id="app">

    <ul class="cards">
      <li v-for="animal in animals">
        <Card :file="animal"/>
      </li>
    </ul>

  </div>
</template>

<script>
import Card from './components/Card.vue'

const animals = [
      'elephant',
      'lion',
      'fox',
      'tiger',
      'rabbit',
      'owl'
      ];

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
  name: 'app',
  components: {
    Card
  },
  data() {
    return {
      animals: dupsShuffled
    }
  }
}

 
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
  // flex-wrap: wrap;
  // justify-content: flex-start;
    grid-gap: 20px;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  // grid-gap: 20px;
  // justify-items: center;
  // align-items: end;
  // width: 100%;
}

li {
  max-width: 100%;
  display: block;
  // width: 25%;
  // margin: 10px;

}

</style>
