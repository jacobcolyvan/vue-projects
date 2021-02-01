<template>
  <div id="board-frame">
    <div
      class="board-row"
      v-for="(row, index) in boardArray"
      :key="index"
    >
      <span
        class="board-point"
        v-for="(point, index) in row"
        :key="index"
      >
        <span> {{ point === 0 ? 'o' : point }}</span>
      </span>
    </div>
  </div>
</template>

<script>
import boardData from '../assets/board.json';

export default {
  name: 'Board',
  components: {},
  props: {
    numberOfPlayers: {
      type: Number,
      required: true
    }
  },
  data () {
    return {
      boardRows: boardData.rowLengths,
      boardArray: []
    }
  },
  methods: {
    createEmptyBoardArray() {
      let tempArray = [];
      this.boardRows.forEach((rowLength) => {
        tempArray.push(Array(rowLength).fill(0));
      });

      this.boardArray = tempArray;
      return tempArray;
    },

    randomisePlayers() {

      let tempBoardArray = this.createEmptyBoardArray();
      //  = this.boardArray;
      const totalBoardRows = 12;
      let playerPositions = [];
      for (let i = 0; i < this.numberOfPlayers; i++) { playerPositions.push([]) }

      const getRandomPlayerPos = () => {
        const playerRow = Math.floor(Math.random() * totalBoardRows);
        const playerCol = Math.floor(Math.random(tempBoardArray[playerRow].length)
                          * tempBoardArray[playerRow].length);
        const playerPos = [playerRow, playerCol];

        return playerPos;
      }

      const addPlayerPositionsToBoard = () => {
        playerPositions.forEach((pos, index) => {
          tempBoardArray[pos[0][0]][pos[0][1]] = index + 1;
          tempBoardArray[pos[1][0]][pos[1][1]] = index + 1;
        })

      }


      for (let i = 0; i < 2; i++ ) {
        for ( let j = 0; j < this.numberOfPlayers; j++ ) {
          let satifiesRequirements = false;

          while ( !satifiesRequirements ) {
            let tempPlayerPos = getRandomPlayerPos();

            let allPointsSatisfy = true;

            playerPositions.flat().forEach((pos) => {
              const neighbours = [[0,0], [-1, -1], [-1, 0], [-1, 1], [0, 1],
                                  [1, 1], [1, 0], [1, -1], [0, -1]];
              neighbours.forEach((neighbour) => {
                const x = tempPlayerPos[0] + neighbour[0];
                const y = tempPlayerPos[1] + neighbour[1];

                const isNeighbourOnBoard = (x >= 0 &&
                                          x < totalBoardRows &&
                                          y >= 0 &&
                                          y < tempBoardArray[tempPlayerPos[0]].length);

                if (isNeighbourOnBoard && (pos[0] === x  && pos[1] === y)) {
                  allPointsSatisfy = false;
                }
              });
            });

            if (allPointsSatisfy) {
              playerPositions[j].push(tempPlayerPos);
              satifiesRequirements = true;
            }
          }
        }
      }

      addPlayerPositionsToBoard();
    }
  },
  mounted() {
    this.randomisePlayers();
  },
  watch: {
    numberOfPlayers () {
      this.randomisePlayers();
    }
  },
}
</script>

<style lang="scss" scoped>
  #board-frame {
    max-width: 500px;
    max-height: 500px;
    width: 90vw;
    height: 90vw;
    border: 1px rgb(62, 62, 66) solid;
    padding: 12px 0;

    display: flex;
    flex-direction: column;

    .board-row {
      height: calc(100% / 12);
      width: 100%;
      text-align: center;
    }

    .board-point {
      display: inline-block;
      width: calc(100% / 6);
      font-size: 12px;
      height: 100%;
      text-align: center;
    }
  }

</style>
