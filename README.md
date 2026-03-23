[2:44 pm, 23/3/2026] mvairamani1983: <!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Ball Poem Mind Map</title>
<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #89f7fe, #66a6ff);
  overflow: hidden;
}.center { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); background: #ffcc00; padding: 20px 30px; border-radius: 50%; text-align: center; font-weight: bold; box-shadow: 0 0 20px rgba(0,0,0,0.3); animation: pulse 2s infinite; }

@keyframes pulse { 0% { transform: translate(-50%, -50%) scale(1); } 50% { transform: translate(-50%, -50%) scale(1.1); } 100% { transform: translate(-50%, -50%) scale(1); } }

.node { position: absolute; padding: 10px 15px; background: white; border-radius: 10px; box-shadow: 0 5px 15px rgba(0,0,0,0.2); animation: float 4s ease-in-out infinite; }

@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }

.line { position: absolute; width: 2px; background: white; transform-origin: top; }

/* Positions */ #theme { top: 10%; left: 45%; } #boy { top: 70%; left: 20%; } #tone { top: 70%; left: 70%; } #symbol { top: 40%; left: 80%; } #message { top: 40%; left: 5%; }

</style>
</head>
<body><div class="center">🎈 The Ball Poem</div><div id="theme" class="node">🌿 Theme<br>Loss, Growth, Reality</div>
<div id="boy" class="node">👦 Boy<br>Innocent → Mature</div>
<div id="tone" class="node">🎭 Tone<br>Sad, Reflective</div>
<div id="symbol" class="node">🎈 Symbol<br>Ball = Childhood</div>
<div id="message" class="node">☀️ Message<br>Accept Loss</div><script>
function connect(div1, div2) {
  const rect1 = div1.getBoundingClientRect();
  const rect2 = div2.getBoundingClientRect();

  const x1 = rect1.left + rect1.width / 2;
  const y1 = rect1.top + rect1.height / 2;
  const x2 = rect2.left + rect2.width / 2;
  const y2 = rect2.top + rect2.height / 2;

  const length = Math.hypot(x2 - x1, y2 - y1);
  const angle = Math.atan2(y2 - y1, x2 - x1) * 180 / Math.PI;

  const line = document.createElement("div");
  line.className = "line";
  line.style.height = length + "px";
  line.style.left = x1 + "px";
  line.style.top = y1 + "px";
  line.style.transform = rotate(${angle}deg);

  document.body.appendChild(line);
}

window.onload = () => {
  const center = document.querySelector('.center');
  connect(center, document.getElementById('theme'));
  connect(center, document.getElementById('boy'));
  connect(center, document.getElementById('tone'));
  connect(center, document.getElementById('symbol'));
  connect(center, document.getElementById('message'));
};
</script></body>
</html>
[2:57 pm, 23/3/2026] mvairamani1983: <!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Animated Ball Poem Mind Map</title>
<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #89f7fe, #66a6ff);
  overflow: hidden;
}.center { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); background: #ffcc00; padding: 25px; border-radius: 50%; text-align: center; font-weight: bold; box-shadow: 0 0 25px rgba(0,0,0,0.4); animation: pulse 2s infinite; cursor: pointer; }

@keyframes pulse { 0% { transform: translate(-50%, -50%) scale(1); } 50% { transform: translate(-50%, -50%) scale(1.15); } 100% { transform: translate(-50%, -50%) scale(1); } }

.node { position: absolute; padding: 12px; background: white; border-radius: 12px; box-shadow: 0 5px 15px rgba(0,0,0,0.2); animation: float 4s ease-in-out infinite; cursor: pointer; }

.node:hover { background: #ffeaa7; transform: scale(1.1); }

@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-12px); } }

.details { display: none; font-size: 12px; margin-top: 5px; }

.line { position: absolute; width: 2px; background: white; transform-origin: top; }

.ball { position: absolute; top: 0; left: 50%; font-size: 30px; animation: fall 3s infinite; }

@keyframes fall { 0% { top: 0; } 100% { top: 90%; opacity: 0; } }

/* Positions */ #theme { top: 10%; left: 45%; } #boy { top: 70%; left: 20%; } #tone { top: 70%; left: 70%; } #symbol { top: 40%; left: 80%; } #message { top: 40%; left: 5%; } #poet { top: 20%; left: 75%; }

</style>
</head>
<body><div class="ball">🎈</div><div class="center" onclick="playSound()">🎈 The Ball Poem</div><div id="theme" class="node" onclick="toggle(this)">
🌿 Theme
<div class="details">Loss, Growth, Responsibility, Reality of Life</div>
</div><div id="boy" class="node" onclick="toggle(this)">
👦 Boy
<div class="details">Innocent → Sad → Thinking → Mature</div>
</div><div id="tone" class="node" onclick="toggle(this)">
🎭 Tone
<div class="details">Sad, Emotional, Reflective</div>
</div><div id="symbol" class="node" onclick="toggle(this)">
🎈 Symbol
<div class="details">Ball = Childhood, Memories, Happiness</div>
</div><div id="message" class="node" onclick="toggle(this)">
☀️ Message
<div class="details">Accept loss, Be strong, Move forward</div>
</div><div id="poet" class="node" onclick="toggle(this)">
✍️ Poet
<div class="details">Observer, Understands emotions, Silent teacher</div>
</div><audio id="sound">
  <source src="https://www.soundjay.com/button/beep-07.wav" type="audio/wav">
</audio><script>
function toggle(el) {
  const detail = el.querySelector('.details');
  detail.style.display = detail.style.display === 'block' ? 'none' : 'block';
}

function playSound() {
  document.getElementById('sound').play();
}

function connect(div1, div2) {
  const rect1 = div1.getBoundingClientRect();
  const rect2 = div2.getBoundingClientRect();

  const x1 = rect1.left + rect1.width / 2;
  const y1 = rect1.top + rect1.height / 2;
  const x2 = rect2.left + rect2.width / 2;
  const y2 = rect2.top + rect2.height / 2;

  const length = Math.hypot(x2 - x1, y2 - y1);
  const angle = Math.atan2(y2 - y1, x2 - x1) * 180 / Math.PI;

  const line = document.createElement("div");
  line.className = "line";
  line.style.height = length + "px";
  line.style.left = x1 + "px";
  line.style.top = y1 + "px";
  line.style.transform = rotate(${angle}deg);

  document.body.appendChild(line);
}

window.onload = () => {
  const center = document.querySelector('.center');
  connect(center, document.getElementById('theme'));
  connect(center, document.getElementById('boy'));
  connect(center, document.getElementById('tone'));
  connect(center, document.getElementById('symbol'));
  connect(center, document.getElementById('message'));
  connect(center, document.getElementById('poet'));
};
</script></body>
</html>
