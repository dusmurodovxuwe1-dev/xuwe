<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tetris O'yini Onlayn - Bepul O'ynash</title>
<meta name="description" content="Klassik Tetris o'yinini onlayn bepul o'ynang. Brauzeringizda to'g'ridan-to'g'ri, ro'yxatdan o'tmasdan o'ynang.">
<meta property="og:title" content="Tetris O'yini Onlayn">
<meta property="og:description" content="Klassik Tetris o'yinini onlayn bepul o'ynang.">
<meta property="og:type" content="website">
<style>
  * { box-sizing: border-box; }
  body {
    margin: 0;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, #1e1b2e, #0d0c1a);
    font-family: 'Segoe UI', Arial, sans-serif;
    color: #eee;
  }
  .wrap {
    display: flex;
    gap: 24px;
    align-items: flex-start;
  }
  canvas {
    background: #100e1c;
    border: 3px solid #6c5ce7;
    border-radius: 8px;
    box-shadow: 0 0 30px rgba(108,92,231,0.4);
  }
  .panel {
    width: 160px;
    display: flex;
    flex-direction: column;
    gap: 16px;
  }
  .box {
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(255,255,255,0.15);
    border-radius: 8px;
    padding: 12px;
  }
  .box h3 {
    margin: 0 0 8px;
    font-size: 13px;
    letter-spacing: 1px;
    text-transform: uppercase;
    color: #a29bfe;
  }
  .box .val {
    font-size: 22px;
    font-weight: bold;
  }
  #next {
    display: block;
    margin: 0 auto;
    background: #100e1c;
    border-radius: 6px;
  }
  .keys {
    font-size: 12px;
    line-height: 1.6;
    color: #ccc;
  }
  button {
    background: #6c5ce7;
    border: none;
    color: white;
    padding: 10px;
    border-radius: 6px;
    font-size: 14px;
    cursor: pointer;
    font-weight: 600;
  }
  button:hover { background: #5b4bd6; }
  #overlay {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.75);
    display: none;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    gap: 12px;
    color: white;
    font-size: 28px;
    text-align: center;
  }
</style>
</head>
<body>

<div class="wrap">
  <canvas id="board" width="240" height="480"></canvas>
  <div class="panel">
    <div class="box">
      <h3>Ball</h3>
      <div class="val" id="score">0</div>
    </div>
    <div class="box">
      <h3>Daraja</h3>
      <div class="val" id="level">1</div>
    </div>
    <div class="box">
      <h3>Keyingi</h3>
      <canvas id="next" width="100" height="100"></canvas>
    </div>
    <div class="box keys">
      <div><b>← →</b> harakat</div>
      <div><b>↑</b> aylantirish</div>
      <div><b>↓</b> tez tushirish</div>
      <div><b>Space</b> darhol tushirish</div>
      <div><b>P</b> pauza</div>
    </div>
    <button id="restartBtn">Qayta boshlash</button>
  </div>
</div>

<div id="overlay">
  <div id="overlayText">O'YIN TUGADI</div>
  <button id="overlayBtn">Qayta boshlash</button>
</div>

<script>
const COLS = 10, ROWS = 20, SIZE = 24;
const canvas = document.getElementById('board');
const ctx = canvas.getContext('2d');
const nextCanvas = document.getElementById('next');
const nextCtx = nextCanvas.getContext('2d');
const scoreEl = document.getElementById('score');
const levelEl = document.getElementById('level');
const overlay = document.getElementById('overlay');
const overlayText = document.getElementById('overlayText');

const COLORS = {
  I: '#00d2ff', O: '#ffe66d', T: '#c56cf0',
  S: '#2ed573', Z: '#ff4757', J: '#5352ed', L: '#ffa502'
};

const SHAPES = {
  I: [[1,1,1,1]],
  O: [[1,1],[1,1]],
  T: [[0,1,0],[1,1,1]],
  S: [[0,1,1],[1,1,0]],
  Z: [[1,1,0],[0,1,1]],
  J: [[1,0,0],[1,1,1]],
  L: [[0,0,1],[1,1,1]]
};

let grid, current, next, score, level, linesCleared, gameOver, paused;
let dropInterval, dropTimer;

function newGrid() {
  return Array.from({length: ROWS}, () => Array(COLS).fill(null));
}

function randomPiece() {
  const keys = Object.keys(SHAPES);
  const key = keys[Math.floor(Math.random() * keys.length)];
  return {
    key,
    shape: SHAPES[key].map(row => row.slice()),
    color: COLORS[key],
    x: Math.floor(COLS / 2) - Math.ceil(SHAPES[key][0].length / 2),
    y: 0
  };
}

function rotate(shape) {
  const rows = shape.length, cols = shape[0].length;
  const res = Array.from({length: cols}, () => Array(rows).fill(0));
  for (let r = 0; r < rows; r++)
    for (let c = 0; c < cols; c++)
      res[c][rows - 1 - r] = shape[r][c];
  return res;
}

function collides(shape, x, y) {
  for (let r = 0; r < shape.length; r++) {
    for (let c = 0; c < shape[r].length; c++) {
      if (!shape[r][c]) continue;
      const nx = x + c, ny = y + r;
      if (nx < 0 || nx >= COLS || ny >= ROWS) return true;
      if (ny >= 0 && grid[ny][nx]) return true;
    }
  }
  return false;
}

function merge() {
  current.shape.forEach((row, r) => {
    row.forEach((val, c) => {
      if (val) {
        const ny = current.y + r, nx = current.x + c;
        if (ny >= 0) grid[ny][nx] = current.color;
      }
    });
  });
}

function clearLines() {
  let cleared = 0;
  for (let r = ROWS - 1; r >= 0; r--) {
    if (grid[r].every(cell => cell)) {
      grid.splice(r, 1);
      grid.unshift(Array(COLS).fill(null));
      cleared++;
      r++;
    }
  }
  if (cleared) {
    const points = [0, 100, 300, 500, 800][cleared] * level;
    score += points;
    linesCleared += cleared;
    level = Math.floor(linesCleared / 10) + 1;
    dropInterval = Math.max(100, 800 - (level - 1) * 70);
    scoreEl.textContent = score;
    levelEl.textContent = level;
  }
}

function spawn() {
  current = next;
  next = randomPiece();
  drawNext();
  if (collides(current.shape, current.x, current.y)) {
    endGame();
  }
}

function endGame() {
  gameOver = true;
  clearInterval(dropTimer);
  overlayText.textContent = `O'YIN TUGADI — Ball: ${score}`;
  overlay.style.display = 'flex';
}

function drawCell(c, x, y, color) {
  c.fillStyle = color;
  c.fillRect(x * SIZE, y * SIZE, SIZE - 1, SIZE - 1);
  c.fillStyle = 'rgba(255,255,255,0.15)';
  c.fillRect(x * SIZE, y * SIZE, SIZE - 1, 4);
}

function draw() {
  ctx.fillStyle = '#100e1c';
  ctx.fillRect(0, 0, canvas.width, canvas.height);

  for (let r = 0; r < ROWS; r++)
    for (let c = 0; c < COLS; c++)
      if (grid[r][c]) drawCell(ctx, c, r, grid[r][c]);

  current.shape.forEach((row, r) => {
    row.forEach((val, c) => {
      if (val) {
        const y = current.y + r;
        if (y >= 0) drawCell(ctx, current.x + c, y, current.color);
      }
    });
  });

  ctx.strokeStyle = 'rgba(255,255,255,0.05)';
  for (let i = 0; i <= COLS; i++) {
    ctx.beginPath(); ctx.moveTo(i * SIZE, 0); ctx.lineTo(i * SIZE, canvas.height); ctx.stroke();
  }
  for (let i = 0; i <= ROWS; i++) {
    ctx.beginPath(); ctx.moveTo(0, i * SIZE); ctx.lineTo(canvas.width, i * SIZE); ctx.stroke();
  }
}

function drawNext() {
  nextCtx.fillStyle = '#100e1c';
  nextCtx.fillRect(0, 0, nextCanvas.width, nextCanvas.height);
  const shape = next.shape;
  const s = 20;
  const offX = (nextCanvas.width - shape[0].length * s) / 2;
  const offY = (nextCanvas.height - shape.length * s) / 2;
  shape.forEach((row, r) => {
    row.forEach((val, c) => {
      if (val) {
        nextCtx.fillStyle = next.color;
        nextCtx.fillRect(offX + c * s, offY + r * s, s - 1, s - 1);
      }
    });
  });
}

function drop() {
  if (gameOver || paused) return;
  if (!collides(current.shape, current.x, current.y + 1)) {
    current.y++;
  } else {
    merge();
    clearLines();
    spawn();
  }
  draw();
}

function hardDrop() {
  while (!collides(current.shape, current.x, current.y + 1)) current.y++;
  merge();
  clearLines();
  spawn();
  draw();
}

function move(dx) {
  if (!collides(current.shape, current.x + dx, current.y)) {
    current.x += dx;
    draw();
  }
}

function rotateCurrent() {
  const rotated = rotate(current.shape);
  let x = current.x;
  if (collides(rotated, x, current.y)) {
    if (!collides(rotated, x - 1, current.y)) x -= 1;
    else if (!collides(rotated, x + 1, current.y)) x += 1;
    else if (!collides(rotated, x - 2, current.y)) x -= 2;
    else if (!collides(rotated, x + 2, current.y)) x += 2;
    else return;
  }
  current.shape = rotated;
  current.x = x;
  draw();
}

function startTimer() {
  clearInterval(dropTimer);
  dropTimer = setInterval(drop, dropInterval);
}

function restart() {
  grid = newGrid();
  score = 0; level = 1; linesCleared = 0;
  gameOver = false; paused = false;
  dropInterval = 800;
  scoreEl.textContent = 0;
  levelEl.textContent = 1;
  overlay.style.display = 'none';
  next = randomPiece();
  spawn();
  draw();
  startTimer();
}

document.addEventListener('keydown', (e) => {
  if (gameOver) return;
  if (e.key === 'p' || e.key === 'P') {
    paused = !paused;
    return;
  }
  if (paused) return;
  switch (e.key) {
    case 'ArrowLeft': move(-1); break;
    case 'ArrowRight': move(1); break;
    case 'ArrowDown': drop(); break;
    case 'ArrowUp': rotateCurrent(); break;
    case ' ': e.preventDefault(); hardDrop(); break;
  }
});

document.getElementById('restartBtn').addEventListener('click', restart);
document.getElementById('overlayBtn').addEventListener('click', restart);

restart();
</script>

</body>
</html>
