<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Cricket App</title>
<style>
body{font-family:Arial;background:#f2f2f2;margin:0}
header{background:#009270;color:white;padding:10px;text-align:center}
.card{background:white;margin:10px;padding:10px;border-radius:5px}
button{padding:6px 10px;background:#009270;color:white;border:none}
.hide{display:none}
</style>
</head>

<body>

<header>🏏 Cricket Live</header>

<div id="home">
  <div class="card">
    <b>Bangladesh vs India</b>
    <p>Bangladesh 145/4 (18.2)</p>
  </div>
  <button onclick="showLogin()">Login</button>
</div>

<div id="login" class="hide">
  <h3>Login</h3>
  <input id="u" placeholder="admin / user"><br><br>
  <input id="p" placeholder="1234"><br><br>
  <button onclick="login()">Login</button>
  <p id="msg"></p>
</div>

<div id="admin" class="hide">
  <h3>Admin Panel</h3>
  <input id="score"><br><br>
  <button onclick="save()">Save</button>
</div>

<div id="user" class="hide">
  <h3>User Dashboard</h3>
  <p id="showScore"></p>
</div>

<script>
function showLogin(){
 home.style.display="none";
 login.style.display="block";
}

function login(){
 if(u.value=="admin" && p.value=="1234"){
  login.style.display="none";
  admin.style.display="block";
 }
 else if(u.value=="user" && p.value=="1234"){
  login.style.display="none";
  showScore.innerText=localStorage.score||"No score";
  user.style.display="block";
 }
 else msg.innerText="Wrong login";
}

function save(){
 localStorage.score=score.value;
 alert("Saved");
}
</script>

</body>
</html>const API_KEY = "PASTE_REAL_KEY";

fetch("https://api.cricapi.com/v1/currentMatches?apikey="+API_KEY)
.then(r=>r.json())
.then(d=>console.log(d));
