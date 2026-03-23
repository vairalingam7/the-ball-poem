<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>The Ball Poem Animation</title>

<style>
body {
  margin: 0;
  overflow: hidden;
  background: linear-gradient(#87CEEB, #1E90FF);
  font-family: Arial;
}

#text {
  position: absolute;
  top: 20px;
  width: 100%;
  text-align: center;
  color: white;
  font-size: 24px;
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
  cursor: pointer;
}
</style>
</head>

<body>

<div id="text">A boy is playing happily with his ball...</div>
<button onclick="nextScene()">Next ▶</button>

<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let step = 0;

/* 🎙️ VOICES */
function speak(text, type="narrator") {
  let s = new SpeechSynthesisUtterance(text);

  if(type === "boy") {
    s.pitch = 2;
    s.rate = 1.2;
  } else {
    s.pitch = 1;
    s.rate = 1;
  }

  speechSynthesis.cancel();
  speechSynthesis.speak(s);
}

/* ⚽ BALL */
let ball = {
  x: 300,
  y: 300,
  r: 20,
  dy: 0
};

/* 🌊 WATER */
let waterLevel = canvas.height * 0.7;
let waveOffset = 0;

/* 🧒 BOY */
let boy = {
  x: 100,
  y: canvas.height - 200,
  step: 0,
  blink: 0
};

/* 🧒 DRAW BOY */
function drawBoy() {
  let x = boy.x;
  let y = boy.y;

  // HEAD
  ctx.beginPath();
  ctx.arc(x, y, 25, 0, Math.PI * 2);
  ctx.fillStyle = "#ffcc99";
  ctx.fill();

  // 👀 EYES (blinking)
  ctx.fillStyle = "black";
  if(boy.blink < 5) {
    ctx.fillRect(x-8,y-5,4,4);
    ctx.fillRect(x+4,y-5,4,4);
  }

  // MOUTH
  ctx.beginPath();
  if(step < 4){
    ctx.arc(x,y+5,8,0,Math.PI);
  } else {
    ctx.arc(x,y+12,8,Math.PI,0);
  }
  ctx.stroke();

  // BODY
  ctx.fillStyle="blue";
  ctx.fillRect(x-10,y+25,20,40);

  // 👋 HANDS
  ctx.beginPath();
  let swing = Math.sin(boy.step) * 15;

  if(step < 3) {
    ctx.moveTo(x-10,y+30);
    ctx.lineTo(x-20 + swing,y+50);

    ctx.moveTo(x+10,y+30);
    ctx.lineTo(x+20 - swing,y+50);
  }
  else if(step === 3) {
    ctx.moveTo(x-10,y+30);
    ctx.lineTo(x-20,y+10);

    ctx.moveTo(x+10,y+30);
    ctx.lineTo(x+20,y+10);
  }
  else {
    ctx.moveTo(x-10,y+30);
    ctx.lineTo(x-10,y+60);

    ctx.moveTo(x+10,y+30);
    ctx.lineTo(x+10,y+60);
  }
  ctx.stroke();

  // 🦵 LEGS
  ctx.beginPath();
  ctx.moveTo(x-5,y+65);
  ctx.lineTo(x-5 + Math.sin(boy.step)*10,y+85);

  ctx.moveTo(x+5,y+65);
  ctx.lineTo(x+5 - Math.sin(boy.step)*10,y+85);
  ctx.stroke();

  boy.step += 0.2;

  // blink timing
  boy.blink++;
  if(boy.blink > 60) boy.blink = 0;
}

/* ⚽ DRAW BALL */
function drawBall() {
  ctx.beginPath();
  ctx.arc(ball.x, ball.y, ball.r, 0, Math.PI * 2);
  ctx.fillStyle = "orange";
  ctx.fill();
}

/* 🌊 WATER */
function drawWater() {
  ctx.fillStyle = "#1E90FF";
  ctx.beginPath();
  ctx.moveTo(0, waterLevel);

  for(let x=0; x<canvas.width; x+=20){
    let y = Math.sin(x*0.02 + waveOffset) * 10;
    ctx.lineTo(x, waterLevel + y);
  }

  ctx.lineTo(canvas.width, canvas.height);
  ctx.lineTo(0, canvas.height);
  ctx.fill();

  waveOffset += 0.05;
}

/* UPDATE */
function update() {

  if(step >= 1 && step <= 2){
    boy.x += 1;
  }

  if(step >= 2){
    ball.dy += 0.5;
    ball.y += ball.dy;
  }

  if(ball.y + ball.r > waterLevel){
    ball.y = waterLevel - ball.r;
    step = 4;
    updateText();
  }
}

/* LOOP */
function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  drawWater();
  drawBall();
  drawBoy();
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
    t.innerHTML="A boy is playing happily with his ball...";
    speak(t.innerHTML,"boy");
  }
  else if(step === 1){
    t.innerHTML="The boy runs after the ball!";
    speak(t.innerHTML,"boy");
  }
  else if(step === 2){
    t.innerHTML="The ball rolls towards the sea 🌊";
    ball.x = 700;
    speak(t.innerHTML);
  }
  else if(step === 3){
    t.innerHTML="Oh no! The ball falls into the water!";
    speak(t.innerHTML);
  }
  else if(step === 4){
    t.innerHTML="The boy feels sad and stops...";
    speak(t.innerHTML,"boy");
  }
  else{
    t.innerHTML="He learns that loss is a part of life.";
    speak(t.innerHTML);
  }
}

/* AUTO START */
setTimeout(() => {
  updateText();
}, 500);

</script>

</body>
</html>
