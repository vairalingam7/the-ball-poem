<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Ball Poem Cartoon Cat Scene</title>

<style>
body {
  margin: 0;
  overflow: hidden;
  background: linear-gradient(#87CEEB, #1E90FF);
}

#text {
  position: absolute;
  top: 20px;
  width: 100%;
  text-align: center;
  color: white;
  font-size: 22px;
  font-weight: bold;
}

button {
  position: absolute;
  bottom: 20px;
  right: 20px;
  padding: 10px;
  background: #ff4081;
  border: none;
  border-radius: 10px;
  color: white;
}

canvas {
  display: block;
}
</style>
</head>

<body>

<div id="text">A playful cat is enjoying with a ball...</div>
<button onclick="nextScene()">Next ▶</button>

<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let step = 0;

/* 🎙️ VOICE */
function speak(text) {
  let s = new SpeechSynthesisUtterance(text);
  s.pitch = 1.8;
  s.rate = 1.2;
  speechSynthesis.cancel();
  speechSynthesis.speak(s);
}

/* ⚽ BALL */
let ball = {
  x: 300,
  y: 350,
  r: 18,
  dx: 2,
  dy: 0
};

/* 🌊 WATER */
let waterLevel = canvas.height * 0.75;
let waveOffset = 0;

/* 🌳 LAND */
let landLevel = canvas.height * 0.75;

/* 🐱 CAT (Tom-style) */
let cat = {
  x: 100,
  y: landLevel - 60,
  step: 0
};

/* 🐱 DRAW CAT */
function drawCat() {
  let x = cat.x;
  let y = cat.y;

  // body
  ctx.fillStyle = "gray";
  ctx.fillRect(x-15, y, 30, 50);

  // head
  ctx.beginPath();
  ctx.arc(x, y-20, 20, 0, Math.PI*2);
  ctx.fill();

  // ears
  ctx.beginPath();
  ctx.moveTo(x-15,y-30);
  ctx.lineTo(x-5,y-50);
  ctx.lineTo(x,y-30);
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(x+15,y-30);
  ctx.lineTo(x+5,y-50);
  ctx.lineTo(x,y-30);
  ctx.fill();

  // eyes
  ctx.fillStyle="white";
  ctx.fillRect(x-10,y-25,8,10);
  ctx.fillRect(x+2,y-25,8,10);

  ctx.fillStyle="black";
  ctx.fillRect(x-8,y-22,3,3);
  ctx.fillRect(x+4,y-22,3,3);

  // tail animation
  ctx.beginPath();
  ctx.moveTo(x+15,y+10);
  ctx.quadraticCurveTo(x+40,y-10 + Math.sin(cat.step)*10, x+20,y+20);
  ctx.stroke();

  cat.step += 0.2;
}

/* ⚽ DRAW BALL */
function drawBall() {
  ctx.beginPath();
  ctx.arc(ball.x, ball.y, ball.r, 0, Math.PI*2);
  ctx.fillStyle="orange";
  ctx.fill();
}

/* 🌳 DRAW LAND */
function drawLand() {
  ctx.fillStyle = "#228B22";
  ctx.fillRect(0, landLevel, canvas.width, canvas.height);
}

/* 🌊 DRAW WATER */
function drawWater() {
  ctx.fillStyle = "#1E90FF";
  ctx.beginPath();
  ctx.moveTo(0, waterLevel);

  for(let x=0; x<canvas.width; x+=20){
    let y = Math.sin(x*0.02 + waveOffset)*10;
    ctx.lineTo(x, waterLevel + y);
  }

  ctx.lineTo(canvas.width, canvas.height);
  ctx.fill();

  waveOffset += 0.05;
}

/* UPDATE */
function update() {

  // Cat chasing ball
  if(step >= 1) {
    cat.x += 1.5;
  }

  // Ball movement
  if(step >= 2) {
    ball.x += ball.dx;
  }

  // Ball falling
  if(step >= 3) {
    ball.dy += 0.5;
    ball.y += ball.dy;
  }

  if(ball.y + ball.r > waterLevel) {
    step = 4;
    updateText();
  }
}

/* LOOP */
function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  drawLand();
  drawWater();
  drawBall();
  drawCat();
  update();

  requestAnimationFrame(animate);
}
animate();

/* STORY */
function nextScene(){
  step++;
  updateText();
}

function updateText(){
  let t = document.getElementById("text");

  if(step === 0){
    t.innerHTML="A playful cat is enjoying with a ball...";
    speak(t.innerHTML);
  }
  else if(step === 1){
    t.innerHTML="The cat runs and plays with the ball!";
    speak(t.innerHTML);
  }
  else if(step === 2){
    t.innerHTML="The ball rolls away towards the sea 🌊";
    speak(t.innerHTML);
  }
  else if(step === 3){
    t.innerHTML="Oh no! The ball falls into the water!";
    speak(t.innerHTML);
  }
  else{
    t.innerHTML="The cat feels sad... Loss teaches a lesson.";
    speak(t.innerHTML);
  }
}

setTimeout(updateText,500);

</script>

</body>
</html>
