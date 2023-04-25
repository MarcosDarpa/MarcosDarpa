const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');
const ROW = 20;
const COL = 10;
const SQ = 30;
const VACANT = 'white'; // cor do espaço vago

// desenha um quadrado
function drawSquare(x, y, color) {
  ctx.fillStyle = color;
  ctx.fillRect(x * SQ, y * SQ, SQ, SQ);

  ctx.strokeStyle = 'black';
  ctx.strokeRect(x * SQ, y * SQ, SQ, SQ);
}

// cria a grade do jogo
let board = [];
for (let r = 0; r < ROW; r++) {
  board[r] = [];
  for (let c = 0; c < COL; c++) {
    board[r][c] = VACANT;
  }
}

// desenha a grade
function drawBoard() {
  for (let r = 0; r < ROW; r++) {
    for (let c = 0; c < COL; c++) {
      drawSquare(c, r, board[r][c]);
    }
  }
}

drawBoard();

// peças e suas cores
const PIECES = [
  [Z, 'red'],
  [S, 'green'],
  [T, 'purple'],
  [O, 'yellow'],
  [L, 'orange'],
  [I, 'cyan'],
  [J, 'blue'],
];

// gerar aleatoriamente uma peça
function randomPiece() {
  let r = (randomN = Math.floor(Math.random() * PIECES.length)); // 0 -> 6
  return new Piece(PIECES[r][0], PIECES[r][1]);
}

let p = randomPiece();

// o objeto Peça
function Piece(tetromino, color) {
  this.tetromino = tetromino;
  this.color = color;

  this.tetrominoN = 0; // começar a partir do primeiro padrão
  this.activeTetromino = this.tetromino[this.tetrominoN];

  // controla a posição da peça
  this.x = 3;
  this.y = -2;
}

// preencher a cor para a peça
Piece.prototype.fill = function (color) {
  for (let r = 0; r < this.activeTetromino.length; r++) {
    for (let c = 0; c < this.activeTetromino.length; c++) {
      // desenhe apenas as partes preenchidas da peça
      if (this.activeTetromino[r][c]) {
        drawSquare(this.x + c, this.y + r, color);
      }
    }
  }
};

// desenhar uma peça na tela
Piece.prototype.draw = function () {
  this.fill(this.color);
};

// apagar a peça
Piece.prototype.unDraw = function () {
  this.fill(VACANT);
};

// mover para baixo a peça
Piece.prototype.moveDown = function () {
  if (!this.collision(0, 1, this.activeTetromino)) {
    this.unDraw();
    this.y++;
    this.draw();
  } else {
    // trave a peça e gere uma nova peça aleatória
    this.lock();
    p = randomPiece();
  }
};

// mover para a esquerda a peça
Piece.prototype.moveLeft = function () {
  if (!this.collision(-

