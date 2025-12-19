<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Live Cricket</title>

<style>
body{margin:0;font-family:Arial;background:#f1f5f9}
header{background:#009270;color:#fff;padding:10px;display:flex;justify-content:space-between}
button{padding:6px 10px;border:none;border-radius:4px;background:#009270;color:#fff}
input{padding:8px;margin:5px;width:90%}
.card{background:#fff;padding:10px;margin:8px;border-radius:6px}
nav{position:fixed;bottom:0;width:100%;background:#fff;display:flex;justify-content:space-around;border-top:1px solid #ccc;padding:6px}
.hide{display:none}
.center{text-align:center;padding-top:40px}
</style>
</head>

<body>

<header>
  <b>cricbuzz</b>
  <button onclick="showLogin()">Login</button>
</header>

<!-- HOME -->
<div id="home">
  <h3 style="padding:10px">Live Matches</h3>
  <div id="matches" style="padding-bottom:60px">Loading...</div>
</div>

<!-- LOGIN -->
<div id="login" class="center hide">
  <h2>Login</h2>
  <input id="user" placeholder="Username">
  <input id="pass" type="password" placeholder="Password">
  <button onclick="login()">Login</button>
  <p id="msg"></p>
  <p>Admin: admin / 1234</p>
  <p>User: user / 1234</p>
</div>

<!-- ADMIN -->
<div id="admin" class="center hide">
  <h2>Admin Panel</h2>
  <input id="scoreInput" placeholder="Enter Live Score">
  <button onclick="saveScore()">Save Score</button><br><br>
  <button onclick="logout()">Logout</button>
</div>

<!-- DASHBOARD -->
<div id="dashboard" class="center hide">
  <h2 id="dashTitle">Live Score</h2>
  <p id="liveScore"></p>
  <button onclick="bangla()">বাংলা</button>
  <button onclick="logout()">Logout</button>
</div>

<nav>
  <span onclick="showHome()">Home</span>
  <span onclick="showLogin()">Login</span>
</nav>

<script>
// 🔴 REAL API KEY বসাও
const API_KEY = "YOUR_API_KEY_HERE";

// LOAD LIVE MATCHES
fetch(`https://api.cricapi.com/v1/currentMatches?apikey=${API_KEY}&offset=0`)
.then(res=>res.json())
.then(data=>{
 let out="";
 if(data.data){
  data.data.forEach(m=>{
   out+=`<div class="card">
    <b>${m.name}</b>
    <p>${m.status}</p>
   </div>`;
  });
 }
 document.getElementById("matches").innerHTML=out || "No live match";
}).catch(()=>{});

// UI FUNCTIONS
function hideAll(){
 home.classList.add("hide");
 login.classList.add("hide");
 admin.classList.add("hide");
 dashboard.classList.add("hide");
}
function showHome(){hideAll();home.classList.remove("hide")}
function showLogin(){hideAll();login.classList.remove("hide")}

// LOGIN LOGIC
function login(){
 if(user.value=="admin" && pass.value=="1234"){
  localStorage.role="admin";
  hideAll();admin.classList.remove("hide");
 }
 else if(user.value=="user" && pass.value=="1234"){
  localStorage.role="user";
  liveScore.innerText=localStorage.score||"No score yet";
  hideAll();dashboard.classList.remove("hide");
 }
 else msg.innerText="Wrong Login";
}

// ADMIN SAVE SCORE
function saveScore(){
 localStorage.score=scoreInput.value;
 alert("Score Saved");
}

// DASHBOARD BANGLA
function bangla(){
 dashTitle.innerText="লাইভ স্কোর";
 liveScore.innerText=localStorage.score||"কোনো স্কোর নেই";
}

// LOGOUT
function logout(){
 localStorage.clear();
 showHome();
}
</script>

</body>
</html>
