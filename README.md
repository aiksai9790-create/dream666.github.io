
<!DOCTYPE html>
<html lang="my">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Dream666 777 Demo</title>
<style>
* { box-sizing: border-box; }

body {
  margin: 0;
  background: #101020;
  color: white;
  font-family: Arial, sans-serif;
  text-align: center;
}

header {
  padding: 24px 10px;
  background: #202040;
  border-bottom: 2px solid gold;
}

h1 {
  color: gold;
  font-size: 38px;
  text-shadow: 0 0 15px gold;
}

.game {
  position: relative;
  overflow: hidden;
  margin: 28px 14px;
  padding: 25px 12px;
  background: linear-gradient(145deg,#302e57,#1d1c3c);
  border: 2px solid #b99b39;
  border-radius: 22px;
  box-shadow: 0 0 22px #a88a3340;
}

.stats {
  display: grid;
  grid-template-columns: repeat(3,1fr);
  gap: 8px;
  margin: 22px 0;
}

.stat {
  padding: 12px 3px;
  background: #17172e;
  border: 1px solid #75612d;
  border-radius: 12px;
}

.stat strong {
  display: block;
  color: gold;
  font-size: 23px;
  margin-top: 8px;
}

.slots {
  display: flex;
  justify-content: center;
  gap: 9px;
  margin: 30px 0;
}

.slot {
  display: grid;
  place-items: center;
  width: 28%;
  max-width: 100px;
  height: 110px;
  background: linear-gradient(white,#dedede);
  color: #17172b;
  border-radius: 14px;
  font-size: 55px;
  font-weight: bold;
  box-shadow: inset 0 -5px 0 #aaa,0 0 12px #ffffff30;
}

.slot.spinning {
  animation: shake .12s infinite;
}

@keyframes shake {
  0% { transform: translateY(-5px); }
  50% { transform: translateY(5px); }
  100% { transform: translateY(-5px); }
}

button {
  padding: 17px 55px;
  border: none;
  border-radius: 14px;
  background: linear-gradient(#ffe77a,#e9b900);
  color: #17120a;
  font-size: 25px;
  font-weight: bold;
  box-shadow: 0 5px 0 #947300,0 0 20px #ffcf35;
}

button:disabled { opacity: .5; }

#result {
  min-height: 45px;
  margin: 30px 0;
  font-size: 25px;
  font-weight: bold;
}

.win {
  color: gold;
  animation: glow .5s infinite alternate;
}

@keyframes glow {
  from { text-shadow: 0 0 5px gold; transform: scale(1); }
  to { text-shadow: 0 0 25px gold; transform: scale(1.08); }
}

#confetti {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
}

.particle {
  position: absolute;
  top: -15px;
  font-size: 23px;
  animation: fall 2s linear forwards;
}

@keyframes fall {
  to { transform: translateY(650px) rotate(600deg); opacity: 0; }
}

.note { color: #ccc; font-size: 13px; }
.home { display: inline-block; margin: 25px; color: gold; }

</style>
</head>

<body>

<header>
<h1>🌟 Dream666 🌟</h1>
<p>777 Lucky Demo Game</p>
</header>

<div class="game">

<div id="confetti"></div>

<h2>🎰 Lucky 777</h2>
<p>ကံစမ်းပြီး ဂဏန်း ၃ လုံး လှည့်ကြည့်ပါ</p>

<div class="stats">
<div class="stat">
SPIN
<strong id="spins">0</strong>
</div>
<div class="stat">
POINTS
<strong id="points">0</strong>
</div>
<div class="stat">
JACKPOT
<strong id="wins">0</strong>
</div>
</div>

<div class="slots">
<div class="slot" id="s1">7</div>
<div class="slot" id="s2">7</div>
<div class="slot" id="s3">7</div>
</div>

<button id="spin" onclick="spin()">SPIN</button>

<div id="result">✨ GOOD LUCK ✨</div>

<p class="note">
Dream666 Demo Game သာဖြစ်သည်။
ငွေကြေးနှင့် လောင်းကြေးမပါဝင်ပါ။
</p>
</div>

<a class="home" href="./">← Home ပြန်သွားမယ်</a>

<script>
let data = {
  spins: 0,
  points: 0,
  wins: 0
};

try {
  const saved = JSON.parse(localStorage.getItem("dream666data"));
  if (saved) data = {
    spins: Number(saved.spins) || 0,
    points: Number(saved.points) || 0,
    wins: Number(saved.wins) || 0
  };
} catch(e) {}

function update() {
  document.getElementById("spins").textContent = data.spins;
  document.getElementById("points").textContent = data.points;
  document.getElementById("wins").textContent = data.wins;
  localStorage.setItem("dream666data", JSON.stringify(data));
}

update();

let busy = false;

function celebrate() {
  const area = document.getElementById("confetti");
  area.innerHTML = "";

  for(let i=0;i<35;i++) {
    const p = document.createElement("span");
    p.className = "particle";
    p.textContent = ["✨","⭐","🎉","💛"][i%4];
    p.style.left = Math.random()*100+"%";
    p.style.animationDelay = Math.random()+"s";
    area.appendChild(p);
  }

  setTimeout(() => area.innerHTML="",3000);
}

function spin() {
  if(busy) return;
  busy = true;

  const btn = document.getElementById("spin");
  const result = document.getElementById("result");

  const slots = [
    document.getElementById("s1"),
    document.getElementById("s2"),
    document.getElementById("s3")
  ];

  btn.disabled = true;
  result.className = "";
  result.textContent = "🎰 လှည့်နေသည်...";

  slots.forEach(s => s.classList.add("spinning"));

  let count = 0;

  const timer = setInterval(() => {
    slots.forEach(s => {
      s.textContent = Math.floor(Math.random()*10);
    });

    count++;

    if(count >= 18) {
      clearInterval(timer);

      const numbers = [
        Math.floor(Math.random()*10),
        Math.floor(Math.random()*10),
        Math.floor(Math.random()*10)
      ];

      slots.forEach((s,i) => {
        s.textContent = numbers[i];
        s.classList.remove("spinning");
      });

      data.spins++;
      data.points += 1;

      if(numbers.every(n => n===7)) {
        data.wins++;
        data.points += 100;
        result.textContent = "🎉 JACKPOT 777! 🎉";
        result.className = "win";
        celebrate();
      } else {
        result.textContent = "TRY AGAIN! 🍀";
      }

      update();
      btn.disabled = false;
      busy = false;
    }
  },100);
}
</script>

</body>
</html>
