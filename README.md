 <!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Advanced Casino</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body{margin:0;font-family:Arial;background:#0b0b0b;color:#fff}
header{background:#111;padding:15px;display:flex;justify-content:space-between;align-items:center}
h1{color:gold;margin:0}
nav button{margin:3px;background:#222;color:#fff;border:1px solid gold}
button{padding:10px 15px;background:gold;border:none;font-weight:bold;cursor:pointer}
input{padding:10px;width:100%;margin:5px 0}
.section{padding:20px}
.card{background:#1c1c1c;padding:20px;border-radius:10px;max-width:450px;margin:auto}
.hidden{display:none}
.wallet{text-align:center;font-size:20px;margin-bottom:10px}
.log{font-size:13px;max-height:120px;overflow:auto;background:#111;padding:10px}
</style>
</head>

<body>

<header>
<h1>FULL CASINO</h1>
<div>💰 <span id="bal">0</span></div>
</header>

<nav class="section hidden" id="menu">
<button onclick="show('dash')">🏠 Dashboard</button>
<button onclick="show('wallet')">💰 Wallet</button>
<button onclick="show('games')">🎮 Games</button>
<button onclick="show('bonus')">🎁 Bonus</button>
<button onclick="show('history')">📜 History</button>
<button onclick="logout()">Logout</button>
</nav>

<!-- LOGIN -->
<div class="section" id="auth">
<div class="card">
<h2>Login / Register</h2>
<input id="u" placeholder="Username">
<input id="p" type="password" placeholder="Password">
<button onclick="login()">Enter</button>
<p style="font-size:12px;color:#aaa">18+ | Fake money only</p>
</div>
</div>

<!-- DASHBOARD -->
<div class="section hidden" id="dash">
<div class="card">
<h2>Welcome to Casino 🎰</h2>
<p>Play games, win bonuses, enjoy demo casino.</p>
</div>
</div>

<!-- WALLET -->
<div class="section hidden" id="wallet">
<div class="card">
<h3>Wallet</h3>
<input id="amt" type="number" placeholder="Amount">
<button onclick="deposit()">Deposit</button>
<button onclick="withdraw()">Withdraw</button>
</div>
</div>

<!-- GAMES -->
<div class="section hidden" id="games">
<div class="card">
<h3>Games (Bet 100)</h3>
<button onclick="play('Slot',0.2,500)">🎰 Slot</button>
<button onclick="play('Dice',0.5,200)">🎲 Dice</button>
<button onclick="play('Coin',0.5,200)">🪙 Coin Flip</button>
<button onclick="play('Blackjack',0.45,300)">🃏 Blackjack</button>
<button onclick="play('Roulette',0.3,400)">🎡 Roulette</button>
<button onclick="crash()">🚀 Crash</button>
<p id="msg"></p>
</div>
</div>

<!-- BONUS -->
<div class="section hidden" id="bonus">
<div class="card">
<h3>Daily Bonus</h3>
<button onclick="bonus()">🎁 Claim 500</button>
</div>
</div>

<!-- HISTORY -->
<div class="section hidden" id="history">
<div class="card">
<h3>History</h3>
<div class="log" id="hist"></div>
</div>
</div>

<script>
let user=null;

function login(){
 if(!u.value||!p.value)return alert("Fill all");
 let d=JSON.parse(localStorage.getItem(u.value));
 if(!d){d={p:p.value,b:1000,h:[]};localStorage.setItem(u.value,JSON.stringify(d));}
 if(d.p!==p.value)return alert("Wrong password");
 user=u.value;
 auth.classList.add("hidden");
 menu.classList.remove("hidden");
 show('dash');
 render();
}

function show(id){
 document.querySelectorAll('.section').forEach(s=>s.classList.add('hidden'));
 menu.classList.remove("hidden");
 document.getElementById(id).classList.remove("hidden");
}

function render(){
 let d=JSON.parse(localStorage.getItem(user));
 bal.innerText=d.b;
 hist.innerHTML=d.h.slice(-15).reverse().join("<br>");
}

function save(d){localStorage.setItem(user,JSON.stringify(d));render();}

function deposit(){
 let a=+amt.value;
 let d=JSON.parse(localStorage.getItem(user));
 d.b+=a; d.h.push("Deposit +"+a); save(d);
}

function withdraw(){
 let a=+amt.value;
 let d=JSON.parse(localStorage.getItem(user));
 if(a>d.b)return alert("Low balance");
 d.b-=a; d.h.push("Withdraw -"+a); save(d);
}

function play(n,c,w){
 let d=JSON.parse(localStorage.getItem(user));
 if(d.b<100)return alert("Low balance");
 d.b-=100;
 if(Math.random()<c){d.b+=w;msg.innerText=n+" WIN +"+w;d.h.push(n+" Win +"+w);}
 else{msg.innerText=n+" Lose";d.h.push(n+" Lose -100");}
 save(d);
}

function crash(){
 let d=JSON.parse(localStorage.getItem(user));
 if(d.b<100)return alert("Low balance");
 let m=(Math.random()*5).toFixed(2);
 d.b+=Math.floor(m*50);
 d.h.push("Crash x"+m);
 msg.innerText="🚀 Crash x"+m;
 save(d);
}

function bonus(){
 let d=JSON.parse(localStorage.getItem(user));
 d.b+=500; d.h.push("Bonus +500"); save(d);
}

function logout(){location.reload();}
</script>

</body>
</html>
