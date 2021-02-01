<template>
  <div id="main">
    <SelectPlayerAmount
      :numberOfPlayers="numberOfPlayers"
      :playerAmountArray="playerAmountArray"
      @togglePlayerAmount="togglePlayerAmount"
    />
    <Board
      :numberOfPlayers="numberOfPlayers"
    />

  </div>
</template>

<script>
import Board from './components/Board.vue';
import SelectPlayerAmount from './components/SelectPlayerAmount';
// import RandomiseButton from '../components/RandomiseButton';

export default {
  name: 'App',
  components: {
    Board,
    SelectPlayerAmount
  },
  data () {
    return {
      numberOfPlayers: 4,
      playerAmountArray: [2, 3, 4]
    }
  },
  methods: {
    togglePlayerAmount (value) {
      this.numberOfPlayers = value
      console.log(`value changed to ${value}`)
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
  background-color: #928f86;
}

#main {
  height: calc(100vh - 100px);
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
