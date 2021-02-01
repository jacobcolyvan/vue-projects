<template>
  <div id="main">
    <SelectPlayerAmount
      :numberOfPlayers="numberOfPlayers"
      :playerAmountArray="playerAmountArray"
      @togglePlayerAmount="togglePlayerAmount"
    />
    <Board
      :reRandomise="reRandomise"
      :numberOfPlayers="numberOfPlayers"
      @setReRandomiseToFalse="setReRandomiseToFalse"
    />
    <RandomiseButton
      @setReRandomiseToTrue="setReRandomiseToTrue"
    />

  </div>
</template>

<script>
import Board from './components/Board.vue';
import SelectPlayerAmount from './components/SelectPlayerAmount';
import RandomiseButton from './components/RandomiseButton';

export default {
  name: 'App',
  components: {
    Board,
    SelectPlayerAmount,
    RandomiseButton
  },
  data () {
    return {
      numberOfPlayers: 4,
      playerAmountArray: [2, 3, 4],
      reRandomise: false
    }
  },
  methods: {
    togglePlayerAmount (value) {
      this.numberOfPlayers = value
      console.log(`value changed to ${value}`)
    },
    setReRandomiseToTrue () {
      this.reRandomise = true
    },
    setReRandomiseToFalse () {
      this.reRandomise = false
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  margin: 0;
  padding: 0;
  /* background-color: rgb(22, 22, 22);  */
  /* background-color: #FFFAED; */
  background-color: #bebbaf;
}

#main {
  height: calc(100vh - 100px);
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

button {
  background-color: #f5f5f5;
}
</style>
