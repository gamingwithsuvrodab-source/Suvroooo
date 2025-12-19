
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Cricket World</title>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f4f4;
}

/* Navbar */
nav {
  background: #0b5ed7;
  padding: 15px;
  color: white;
}
nav h1 {
  margin: 0;
  display: inline;
}
nav ul {
  list-style: none;
  float: right;
  margin: 0;
}
nav ul li {
  display: inline;
  margin-left: 20px;
}
nav ul li a {
  color: white;
  text-decoration: none;
}

/* Hero */
.hero {
  background: url('https://i.ibb.co/q9Qf3Xg/cricket.jpg') no-repeat center;
  background-size: cover;
  height: 300px;
  color: white;
  text-align: center;
  padding-top: 100px;
}
.hero h2 {
  font-size: 40px;
}

/* Sections */
.container {
  padding: 20px;
}
.card {
  background: white;
  padding: 15px;
  margin-bottom: 15px;
  border-radius: 5px;
}

/* Button */
button {
  background: #0b5ed7;
  color: white;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
}
button:hover {
  background: #084298;
}

/* Footer */
footer {
  background: #222;
  color: white;
  text-align: center;
  padding: 10px;
}
</style>
</head>

<body>

<!-- Navbar -->
<nav>
  <h1>🏏 Cricket World</h1>
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#matches">Matches</a></li>
    <li><a href="#players">Players</a></li>
    <li><a href="#score">Live Score</a></li>
  </ul>
</nav>

<!-- Hero -->
<div class="hero">
  <h2>Welcome to Cricket World</h2>
  <p>All Cricket Updates in One Place</p>
</div>

<!-- Content -->
<div class="container">

  <div class="card" id="matches">
    <h3>🏏 Upcoming Matches</h3>
    <ul>
      <li>Bangladesh vs India</li>
      <li>Australia vs England</li>
      <li>Pakistan vs Sri Lanka</li>
    </ul>
  </div>

  <div class="card" id="players">
    <h3>⭐ Famous Players</h3>
    <p>Shakib Al Hasan, Virat Kohli, Babar Azam, Joe Root</p>
  </div>

  <div class="card" id="score">
    <h3>📊 Live Score</h3>
    <p id="scoreText">Bangladesh: 120/3 (15 overs)</p>
    <button onclick="updateScore()">Update Score</button>
  </div>

</div>

<!-- Footer -->
<footer>
  <p>© 2025 Cricket World | Made with ❤️</p>
</footer>

<script>
function updateScore() {
  document.getElementById("scoreText").innerHTML =
    "Bangladesh: 145/4 (18 overs)";
}
</script>

</body>
</html><!DOCTYPE html>
<html>
<head>
<title>Login</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h2>Login</h2>
<input id="user" placeholder="Username">
<input id="pass" type="password" placeholder="Password">
<button onclick="login()">Login</button>

<p id="msg"></p>

<script src="script.js"></script>
</body>
</html>function login() {
  let user = document.getElementById("user").value;
  let pass = document.getElementById("pass").value;

  if(user === "admin" && pass === "1234") {
    localStorage.setItem("role","admin");
    window.location.href = "admin.html";
  } 
  else if(user === "user" && pass === "1234") {
    localStorage.setItem("role","user");
    window.location.href = "dashboard.html";
  } 
  else {
    document.getElementById("msg").innerText = "Wrong Login!";
  }
}<!DOCTYPE html>
<html>
<head>
<title>Admin Panel</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h1>Admin Panel</h1>
<p>Add Live Score</p>

<input id="scoreInput" placeholder="Enter Score">
<button onclick="saveScore()">Save</button>

<script src="script.js"></script>
</body>
</html>function saveScore(){
  let score = document.getElementById("scoreInput").value;
  localStorage.setItem("liveScore", score);
  alert("Score Updated");
}<!DOCTYPE html>
<html>
<head>
<title>Dashboard</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<h1>🏏 Live Score</h1>
<p id="score"></p>

<button onclick="logout()">Logout</button>

<script>
document.getElementById("score").innerText =
  localStorage.getItem("liveScore") || "No Live Match";

function logout(){
  localStorage.clear();
  window.location.href="login.html";
}
</script>
</body>
</html>body {
  font-family: Arial;
  background:#f4f4f4;
  padding:20px;
}

input, button {
  padding:10px;
  margin:5px;
}

button {
  background:#0b5ed7;
  color:white;
  border:none;
}<button onclick="bangla()">বাংলা</button>

<script>
function bangla(){
  document.body.innerHTML =
  "<h1>ক্রিকেট লাইভ স্কোর</h1><p>"+ 
  localStorage.getItem("liveScore") +
  "</p>";
}
</script>
