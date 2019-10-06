<template>
  <div class="container">
    <div class="board"></div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import $ from "jquery";
import TweenMax from "gsap/TweenMax";
import Draggable from "gsap/Draggable"; 

class Pion{
  constructor(){
    this.div = document.createElement('div');
    this.div.classList.add('pion');
    document.querySelector('.container').appendChild(this.div);
    Draggable.create(".pion", {type:"x,y", edgeResistance:0.65, bounds:".container", throwProps:true});
  }
}
class Cell {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.div = document.createElement("div");
    this.div.style.width = `${100}%`;
    this.div.style.height = `${100}%`;
    this.div.style.border = ".5px solid #333";
    this.div.style.position = "relative";
    this.div.classList.add("cell");
    // Player1
    for (let i = 1; i < 6; i++) {
      if (this.x == 1 && this.y == 8) {
        this.div.classList.add("player1");
      }
      if (this.x == i && this.y == 7) {
        this.div.classList.add("player1");
      }
    }

    // Player2
    for (let i = 9; i < 14; i++) {
      if (this.x == 8 && this.y == 13) {
        this.div.classList.add("player2");
      }
      if (this.x == 7 && this.y == i) {
        this.div.classList.add("player2");
      }
    }

    // Player3
    for (let i = 9; i < 14; i++) {
      if (this.x == 13 && this.y == 6) {
        this.div.classList.add("player3");
      }
      if (this.x == i && this.y == 7) {
        this.div.classList.add("player3");
      }
    }

    // Player4
    for (let i = 1; i < 6; i++) {
      if (this.x == 6 && this.y == 1) {
        this.div.classList.add("player4");
      }
      if (this.x == 7 && this.y == i) {
        this.div.classList.add("player4");
      }
    }
    // Top Left
    for (let i = 0; i < 6; i++) {
      for (let j = 0; j < 6; j++) {
        if (this.x == i) {
          if (this.y == j) {
            this.div.style.border = "0px solid #fff";
            this.div.style.background = "blue";
          }
        }
      }
    }
    // Bottom Right
    for (let i = 9; i < 15; i++) {
      for (let j = 9; j < 15; j++) {
        if (this.x == i) {
          if (this.y == j) {
            this.div.style.border = "0px solid #fff";
            this.div.style.background = "yellow";
          }
        }
      }
    }
    // Top Right
    for (let i = 0; i < 6; i++) {
      for (let j = 9; j < 15; j++) {
        if (this.x == i) {
          if (this.y == j) {
            this.div.style.border = "0px solid #fff";
            this.div.style.background = "green";
          }
        }
      }
    }
    // Bottom Left
    for (let i = 9; i < 15; i++) {
      for (let j = 0; j < 6; j++) {
        if (this.x == i) {
          if (this.y == j) {
            this.div.style.border = "0px solid #fff";
            this.div.style.background = "red";
          }
        }
      }
    }
    // Player 1
    for (let i = 1; i < 5; i++) {
      for (let j = 10; j < 14; j++) {
        if (this.x == i && this.y == j) {
          this.div.style.background = "#fff";
        }
      }
    }
    // Player 2
    for (let i = 10; i < 14; i++) {
      for (let j = 10; j < 14; j++) {
        if (this.x == i && this.y == j) {
          this.div.style.background = "#fff";
        }
      }
    }

    // Player 3
    for (let i = 10; i < 14; i++) {
      for (let j = 1; j < 5; j++) {
        if (this.x == i && this.y == j) {
          this.div.style.background = "#fff";
        }
      }
    }

    // Player 3
    for (let i = 1; i < 5; i++) {
      for (let j = 1; j < 5; j++) {
        if (this.x == i && this.y == j) {
          this.div.style.background = "#fff";
        }
      }
    }

    // Player 3
    for (let i = 6; i < 9; i++) {
      for (let j = 6; j < 9; j++) {
        if (this.x == i && this.y == j) {
          this.div.style.border = "0px solid #fff";
        }
      }
    }
    document.querySelector(".board").appendChild(this.div);
    this.div.addEventListener("click", () => {
      alert(`x:${x} y:${y}`);
    });
  }
  getPosition() {}
}
class Board {
  constructor(X, Y) {
    this.X = Y;
    this.Y = Y;
  }
  createBoard() {
    let squares = new Array();
    for (let i = 0; i < this.X; i++) {
      squares[i] = new Array();
      for (var j = 0; j < this.Y; j++) {
        squares[i].push(new Cell(i, j));
        console.log(`x: ${i} y:${j}`);
      }
    }
  }
}
export default {
  components: {
    Logo
  },
  mounted() {
    const board = new Board(15, 15);
    board.createBoard();
    new Pion();
  }
};
</script>

<style lang="scss">
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background-image: linear-gradient(
    to right bottom,
    rgb(3, 77, 119),
    rgb(6, 112, 173)
  );
}
.board {
  background: #2c2929;
  display: grid;
  grid-template-columns: repeat(15, 2.5rem);
  grid-template-rows: repeat(15, 2.5rem);
}
.cell {
  background: #fff;
}
.player1 {
  background: green;
}
.player2 {
  background: yellow;
}
.player3 {
  background: red;
}
.player4 {
  background: blue;
}
.pion{
  width: 2rem;
  height: 2rem;
  background: yellow;
  border-radius: 50%;
  border: 2px solid #333;
  cursor: grab !important;
  &:active{
    cursor: grabbing !important;
  }
}
</style>
