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
        o
      </span>
    </div>
  </div>
</template>

<script>
import boardData from '../assets/board.json';

export default {
  name: 'Board',
  components: {},
  data () {
    return {
      boardRows: boardData.rowLengths,
      boardArray: [],
      playerPositionsByColour: {
        "orange": [],
        "red": [],
        "blue": []
      }
    }
  },
  methods: {
    createEmptyBoardArray() {
      let tempArray = [];
      this.boardRows.forEach((rowLength) => {
        tempArray.push(Array(rowLength).fill(0));
      });

      this.boardArray = tempArray;
    },

    randomisePlayers() {
      let tempBoardArray = this.boardArray;
      const totalBoardRows = 12;
      let playerPositions = [[], [], []];

      const getRandomPlayerPos = () => {
        const playerRow = Math.floor(Math.random() * totalBoardRows);
        const playerCol = Math.floor(Math.random(tempBoardArray[playerRow].length) * tempBoardArray[playerRow].length);
        const playerPos = [playerRow, playerCol];

        return playerPos;
      }

      const addPlayerPositionsToObject = () => {
        let tempPlayerPositionsByColour = this.playerPositionsByColour
        Object.entries(tempPlayerPositionsByColour).forEach(([colour], index) => {
          tempPlayerPositionsByColour[colour] = playerPositions[index];
        });

        this.playerPositionsByColour = tempPlayerPositionsByColour;
        console.log("positions added", tempPlayerPositionsByColour);
      }


      for (let i = 0; i < 2; i++ ) {
        for ( let j = 0; j < 3; j++ ) {
          let satifiesRequirements = false;

          while ( !satifiesRequirements ) {
            let tempPlayerPos = getRandomPlayerPos();

            let allPointsSatisfy = true;

            playerPositions.flat().forEach((pos) => {
              const neighbours = [[0,0], [-1, -1], [-1, 0], [-1, 1], [0, 1], [1, 1], [1, 0], [1, -1], [0, -1]];
              neighbours.forEach((neighbour) => {
                const x = tempPlayerPos[0] + neighbour[0];
                const y = tempPlayerPos[1] + neighbour[1];

                const isNeighbourOnBoard = (x >= 0 &&
                                          x < totalBoardRows &&
                                          y >= 0 &&
                                          y < tempBoardArray[tempPlayerPos[0]].length);

                if (isNeighbourOnBoard && (pos[0] === x  && pos[1] === y)) {
                  console.log("nup!")
                  allPointsSatisfy = false;
                }
              });
            });

            if (allPointsSatisfy) {
              console.log("added", j)
              playerPositions[j].push(tempPlayerPos);
              satifiesRequirements = true;
            }
          }
        }
      }

      addPlayerPositionsToObject();
    }

  },
  mounted() {
    this.createEmptyBoardArray()
  },
  watch: {
    boardArray() {
      console.log('board made!')
      this.randomisePlayers();
    },
    playerPositionsByColour() {
      console.log('playerPositionsByColourvsf', this.playerPositionsByColour);
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
      display: flex;
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
