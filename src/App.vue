<template>
  <div id="app">
    <Header title="Card Match" />
    <Nav 
      :matched="matched" 
      :winner="winner"
      :total="cardArray.length"
      @clickNewGame="createNewGame(24,100,200)"
    />
    <CardContainer 
      :cardArray="cardArray"
      @clickCard="flipCard"
      @clickNewGame="createNewGame(24,100,200)"
    />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Nav from './components/Nav.vue'
import CardContainer from './components/CardContainer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Nav,
    CardContainer
  },
  data: () => {
    return {
      matched: 0,
      cardArray: [],
      matchedIds: [],
      firstCardId: '',
      secondCardId: '',
      winner: false
    }
  },
  methods: {
    createNewGame: function(num, low, high) {
      this.matched = 0;
      this.matchedIds = [];
      this.firstCardId = '';
      this.secondCardId = '';
      this.winner = false;
      const result = [];
      const numSet = new Set();

      while (result.length < num) {
        const randomNum = Math.floor(Math.random() * (high - low + 1) + low);

        if (!numSet.has(randomNum)) {
          numSet.add(randomNum);
          result.push({ name: randomNum, isShown: false, card: 1 });
          result.push({ name: randomNum, isShown: false, card: 2 });
        }
      }

      this.cardArray = this.shuffleFisherYates(result);
    },
    shuffleFisherYates: function(arr) {
      let currIdx = arr.length;
      let tempValue;
      let randomIdx;

      while (0 !== currIdx) {
        randomIdx = Math.floor(Math.random() * currIdx);
        currIdx--;

        // swap 
        tempValue = arr[currIdx];
        arr[currIdx] = arr[randomIdx];
        arr[randomIdx] = tempValue;
      }

      return arr;
    },
    flipCard: function(event) {
      const id = event.currentTarget.id;

      if (this.firstCardId === id || this.secondCardId === id) return;
      if (this.matchedIds.indexOf(id) >= 0) return;

      if (!this.firstCardId) {
        this.firstCardId = id;
        this.updateCardArray(id, true);
      } else {
        this.secondCardId = id;
        this.updateCardArray(id, true);
        this.checkForMatch();

        if (this.matched === this.cardArray.length/2) {
          this.winner = true;
          this.cardArray = [];
          this.matched = 0;
          this.matchedIds.push(this.firstCardId)
          this.matchedIds.push(this.secondCardId)
        }

        this.firstCardId = '';
        this.secondCardId = '';
      } 
    },
    updateCardArray: function(id, bool) {
      this.cardArray[id].isShown = bool;
    },
    checkForMatch: function() {
      const arr = this.cardArray;
      const id1 = this.firstCardId;
      const id2 = this.secondCardId;

      if (arr[id1].name !== arr[id2].name) {
        setTimeout(() => {
          this.updateCardArray(id1, false);
          this.updateCardArray(id2, false);
        }, 1000)
      } else {
        this.matched++;
      }
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

#app {
  height: 100vh;
  background: black;
}
</style>
