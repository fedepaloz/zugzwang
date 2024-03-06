<script>
export default {
  data() {
    return {
      isClicked: false,
      pippo: '',
      validMoves: [],
      availableRows: [0, 1, 2, 3, 4, 5, 6, 7],
      availableCells: [0, 1, 2, 3, 4, 5, 6, 7],
      availableMoves: [
        [-2, -1],
        [-2, 1],
        [-1, -2],
        [-1, 2],
        [1, -2],
        [1, 2],
        [2, -1],
        [2, 1]
      ],
      selectedCell: null
    }
  },
  methods: {
    horseCheck(values) {
      this.validMoves = []
      let valueOne = values[0]
      let valueTwo = values[1]
      this.selectedCell = values[0] + ',' + values[1]
      this.availableMoves.forEach((el) => {
        const newPositionOne = (valueOne + el[0]).toString()
        const newPositionTwo = (valueTwo + el[1]).toString()
        const pippo = newPositionOne + newPositionTwo
        this.validMoves.push(pippo)
      })
    },
    calculateClass(row, col) {
      let classes = ''
      if ((row + col) % 2 === 0) {
        classes = ' square-white'
      } else {
        classes = 'square-black'
      }

      return classes
    },

    isMoveValid(row, cell) {
      return this.validMoves.includes(row.toString() + cell.toString())
    },
    isActive(row, cell) {
      return this.selectedCell === row + ',' + cell
    }
  }
}
</script>

<template>
  <body>
    <div class="chessboard">
      <div class="row" v-for="row in availableRows" v-bind:value="row" v-bind:key="row">
        <div v-for="cell in availableCells" v-bind:value="cell" v-bind:key="cell">
          <div
            @click="horseCheck([row, cell])"
            :class="[
              calculateClass(row, cell),
              isMoveValid(row, cell) ? 'square-horse' : '',
              isActive(row, cell) ? 'red' : ''
            ]"
            class="square"
          >
            {{ row.toString() + '-' + cell.toString() }}
          </div>
        </div>
      </div>
    </div>
    <div></div>
  </body>
</template>

<style scoped>
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  background-color: #f0f0f0;
}

.chessboard {
  border: 2px solid #333;
}

.row {
  display: flex;
}

.square {
  width: 50px;
  height: 50px;
}
.square-white {
  background-color: white;
  color: black;
}
.square-black {
  background-color: black;
  color: white;
}
.red {
  background-color: red;
}
.square-horse {
  background-color: green;
}
</style>
