<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>The Ball Poem Story</title>

<style>
body {
  margin: 0;
  overflow: hidden;
  font-family: Arial;
  background: linear-gradient(#87CEEB, #1E90FF);
}

#story {
  position: absolute;
  top: 20px;
  width: 100%;
  text-align: center;
  color: white;
  font-size: 22px;
  font-weight: bold;
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

<div id="story">A boy is playing happily with his ball...</div>
<button onclick="nextScene()">Next ▶</button>

<canvas id="canvas"></canvas>

<audio id="splash" src="https://www.soundjay.com/water/sounds/water-splash-1.mp3"></audio>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let step = 0;

let ball = {
  x: 200,
  y: 100,
  radius: 20,
  dy: 0,
  gravity: 0.5
};

let waterLevel = canvas.height * 0.7;
let waves = [];

function drawBoy() {
  ctx.font = "50px Arial";
  if(step < 3) {
    ctx.fillText("😊", 50, canvas.height - 200);
  } else {
    ctx.fillText("😢", 50, canvas.height - 200);
  }
}

function drawBall() {
  ctx.beginPath();
  ctx.arc(ball.x, ball.y, ball.radius, 0, Math.PI * 2);
  ctx.fillStyle = "orange";
  ctx.fill();
}

function drawWater() {
  ctx.fillStyle = "#1E90FF";
  ctx.fillRect(0, waterLevel, canvas.width, canvas.height);

  ctx.beginPath();
  ctx.moveTo(0, waterLevel);
  for (let w of waves) {
    ctx.quadraticCurveTo(w.x, waterLevel + w.height, w.x + 50, waterLevel);
  }
  ctx.lineTo(canvas.width, canvas.height);
  ctx.fill();
}

function update() {
  if(step >= 2) {
    ball.dy += ball.gravity;
    ball.y += ball.dy;
  }

  if(ball.y + ball.radius > waterLevel) {
    ball.y = waterLevel - ball.radius;
    waves.push({x: ball.x, height: 20});
    document.getElementById("splash").play();
    step = 3;
    updateStory();
  }

  waves.forEach(w => w.height *= 0.95);
}

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  drawWater();
  drawBall();
  drawBoy();
  update();

  requestAnimationFrame(draw);
}

function nextScene() {
  step++;
  updateStory();
}

function updateStory() {
  let text = document.getElementById("story");

  if(step === 0) text.innerHTML = "A boy is playing happily with his ball...";
  else if(step === 1) text.innerHTML = "The ball rolls towards the sea...";
  else if(step === 2) text.innerHTML = "The ball falls into the water 🌊";
  else if(step === 3) text.innerHTML = "The boy feels sad and helpless 😢";
  else text.innerHTML = "He learns about loss and growing up.";
}

draw();
</script>

</body>
</html>
