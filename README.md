- 👋 Hi, I’m @MarcosDarpa
- 👀 I’m interested in ...## Bem-vindo ao meu GitHub!

### Sobre mim
Olá, estou em uma jornada para me tornar um programador habilidoso e apaixonado pelo que faço. Estou sempre buscando novos desafios e aprendendo novas tecnologias.

### Habilidades e Tecnologias
- HTML5
- CSS3
- JavaScript
- ...

### Projetos em destaque
- site-image

- ...

### Frase motivadora
"Nunca é tarde para aprender algo novo. Comece hoje mesmo a sua jornada na programação e conquiste o mundo com suas habilidades!"
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
