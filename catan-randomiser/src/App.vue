<template>
  <div id="main">
    <Board />

  </div>
</template>

<script>
import Board from './components/Board.vue';

export default {
  name: 'App',
  components: {
    Board
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
}
</style>
