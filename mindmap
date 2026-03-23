<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Ball Poem Game</title>

<style>
body {
  margin: 0;
  overflow: hidden;
  font-family: Arial;
  background: linear-gradient(#87CEEB, #1E90FF);
}

#story {
  position: absolute;
  top: 10px;
  width: 100%;
  text-align: center;
  color: white;
  font-size: 22px;
  font-weight: bold;
}

#score {
  position: absolute;
  top: 50px;
  left: 20px;
  color: white;
  font-size: 18px;
}

canvas {
  display: block;
}

button {
  position: absolute;
  bottom: 20px;
  right: 20px;
  padding: 10px;
  border: none;
  background: #ff4081;
  color: white;
  border-radius: 10px;
  cursor: pointer;
}
</style>
</head>

<body>

<div id="story">Catch the ball before it falls into the sea!</div>
<div id="score">Score: 0</div>

<canvas id="canvas"></canvas>

<button onclick="startGame()">Start Game 🎮</button>

<audio id="splash" src="https://www.soundjay.com/water/sounds/water-splash-1.mp3"></audio>
<audio id="catch" src="https://www.soundjay.com/button/sounds/button-09.mp3"></audio>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let ball, paddle, score, gameRunning;

let waterLevel = canvas.height * 0.75;
let waves = [];

function init() {
  ball = {
    x: canvas.width / 2,
    y: 100,
    radius: 20,
    dy: 0,
    gravity: 0.5
  };

  paddle = {
    x: canvas.width / 2 - 60,
    y: canvas.height - 120,
    width: 120,
    height: 15
  };

  score = 0;
  gameRunning = true;
}

function drawBall() {
  ctx.beginPath();
  ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
  ctx.fillStyle = "orange";
  ctx.fill();
}

function drawPaddle() {
  ctx.fillStyle = "white";
  ctx.fillRect(paddle.x, paddle.y, paddle.width, paddle.height);
}

function drawWater() {
  ctx.fillStyle = "#1E90FF";
  ctx.fillRect(0, waterLevel, canvas.width, canvas.height);

  ctx.beginPath();
  ctx.moveTo(0, waterLevel);
  for (let i = 0; i < waves.length; i++) {
    let w = waves[i];
    ctx.quadraticCurveTo(w.x, waterLevel + w.height, w.x + 50, waterLevel);
  }
  ctx.lineTo(canvas.width, canvas.height);
  ctx.lineTo(0, canvas.height);
  ctx.fill();
}

function update() {
  if (!gameRunning) return;

  ball.dy += 0.5;
  ball.y += ball.dy;

  // Paddle collision
  if (
    ball.y + ball.radius > paddle.y &&
    ball.x > paddle.x &&
    ball.x < paddle.x + paddle.width
  ) {
    ball.dy = -10;
    score++;
    document.getElementById("score").innerHTML = "Score: " + score;
    document.getElementById("catch").play();
  }

  // Water collision
  if (ball.y + ball.radius > waterLevel) {
    gameRunning = false;

    waves.push({ x: ball.x, height: 30 });
    document.getElementById("splash").play();

    document.getElementById("story").innerHTML =
      "The ball is lost... The boy learns about loss 💔";
  }

  // Wave fade
  for (let i = 0; i < waves.length; i++) {
    waves[i].height *= 0.95;
  }
}

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  drawWater();
  drawBall();
  drawPaddle();
  update();

  requestAnimationFrame(draw);
}

// Control paddle
document.addEventListener("mousemove", (e) => {
  paddle.x = e.clientX - paddle.width / 2;
});

document.addEventListener("touchmove", (e) => {
  paddle.x = e.touches[0].clientX - paddle.width / 2;
});

function startGame() {
  init();
  document.getElementById("story").innerHTML =
    "Save the ball! Don't let it fall 🌊";
}

draw();
</script>

</body>
</html>
