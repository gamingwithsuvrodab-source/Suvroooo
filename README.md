<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>FULL CASINO SYSTEM</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<style>
body{margin:0;font-family:Arial;background:#0b0b0b;color:#fff}
header{background:#111;padding:15px 25px;display:flex;justify-content:space-between}
h1{color:gold;margin:0}
button{padding:10px 15px;background:gold;border:none;font-weight:bold;cursor:pointer}
input{padding:10px;width:100%;margin:5px 0}
.section{padding:25px}
.card{background:#1c1c1c;padding:20px;border-radius:10px;max-width:420px;margin:auto}
.hidden{display:none}
.wallet{text-align:center;font-size:20px;margin-bottom:15px}
.log{font-size:13px;max-height:120px;overflow:auto;background:#111;padding:10px}
</style>
</head>

<body>

<header>
<h1>FULL CASINO</h1>
<button onclick="logout()">Logout</button>
</header>

<!-- AUTH -->
<div class="section" id="auth">
<div class="card">
<h2>Login / Register</h2>
<input id="u" placeholder="Username">
<input id="p" type="password" placeholder="Password">
<button onclick="login()">Enter</button>
<p style="font-size:12px;color:#aaa">18+ | Fake money only</p>
</div>
</div>

<!-- USER PANEL -->
<div class="section hidden" id="userPanel">
<div class="wallet">💰 Balance: <span id="bal">0</span></div>

<div class="card">
<h3>Wallet</h3>
<input id="amt" type="number" placeholder="Amount">
<button onclick="deposit()">Deposit</button>
<button onclick="withdraw()">Withdraw</button>
</div>

<br>

<div class="card">
<h3>Games (Bet 100)</h3>
<button onclick="play('Slot',0.2,500)">🎰 Slot</button>
<button onclick="play('Dice',0.5,200)">🎲 Dice</button>
<button onclick="play('Coin',0.5,200)">🪙 Coin Flip</button>
<p id="msg"></p>
</div>

<br>

<div class="card">
<h3>History</h3>
<div class="log" id="hist"></div>
</div>
</div>

<!-- ADMIN PANEL -->
<div class="section hidden" id="adminPanel">
<div class="card">
<h2>ADMIN PANEL</h2>
<input id="target" placeholder="Username">
<input id="adminAmt" type="number" placeholder="Amount">
<button onclick="addBal()">Add Balance</button>
<button onclick="resetBal()">Reset Balance</button>
</div>
</div>

<script>
let currentUser=null;

function login(){
 if(!u.value || !p.value) return alert("Fill all");
 let d = JSON.parse(localStorage.getItem(u.value));
 if(!d){
   d={pass:p.value,bal:1000,h:[]};
   localStorage.setItem(u.value,JSON.stringify(d));
 }
 if(d.pass!==p.value) return alert("Wrong password");

 currentUser=u.value;
 auth.classList.add("hidden");

 if(currentUser==="admin"){
   adminPanel.classList.remove("hidden");
 }else{
   userPanel.classList.remove("hidden");
   render();
 }
}

function render(){
 let d=JSON.parse(localStorage.getItem(currentUser));
 bal.innerText=d.bal;
 hist.innerHTML=d.h.slice(-10).reverse().join("<br>");
}

function save(d){
 localStorage.setItem(currentUser,JSON.stringify(d));
 render();
}

function deposit(){
 let a=+amt.value;
 if(a<=0) return;
 let d=JSON.parse(localStorage.getItem(currentUser));
 d.bal+=a;
 d.h.push("Deposit +"+a);
 save(d);
}

function withdraw(){
 let a=+amt.value;
 let d=JSON.parse(localStorage.getItem(currentUser));
 if(a>d.bal) return alert("Low balance");
 d.bal-=a;
 d.h.push("Withdraw -"+a);
 save(d);
}

function play(name,chance,win){
 let d=JSON.parse(localStorage.getItem(currentUser));
 if(d.bal<100) return alert("Low balance");
 d.bal-=100;
 if(Math.random()<chance){
   d.bal+=win;
   msg.innerText="🎉 "+name+" WIN +"+win;
   d.h.push(name+" Win +"+win);
 }else{
   msg.innerText="❌ "+name+" Lose";
   d.h.push(name+" Lose -100");
 }
 save(d);
}

function addBal(){
 let t=target.value;
 let a=+adminAmt.value;
 let d=JSON.parse(localStorage.getItem(t));
 if(!d) return alert("User not found");
 d.bal+=a;
 localStorage.setItem(t,JSON.stringify(d));
 alert("Balance added");
}

function resetBal(){
 let t=target.value;
 let d=JSON.parse(localStorage.getItem(t));
 if(!d) return alert("User not found");
 d.bal=1000;
 d.h=[];
 localStorage.setItem(t,JSON.stringify(d));
 alert("Reset done");
}

function logout(){
 location.reload();
}
</script>

</body>
</html>
