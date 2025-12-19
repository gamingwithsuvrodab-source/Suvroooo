cricket-live/
│── index.html
│── style.css
│── script.js
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Live Cricket Score</title>
<link rel="stylesheet" href="style.css">
</head>

<body>

<!-- HEADER -->
<header class="topbar">
  <div class="menu">☰</div>
  <div class="logo">cricbuzz</div>
  <button class="appbtn">GET APP</button>
</header>

<!-- MATCH LIST -->
<div class="content">
  <h3 class="section-title">Live Matches</h3>
  <div id="matches">
    <p>Loading live matches...</p>
  </div>
</div>

<!-- BOTTOM NAV -->
<nav class="bottom-nav">
  <span>Home</span>
  <span>Matches</span>
  <span>Series</span>
  <span>Videos</span>
  <span>News</span>
</nav>

<script src="script.js"></script>
</body>
</html>body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f1f5f9;
}

.topbar {
  background: #009270;
  color: white;
  padding: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.logo {
  font-weight: bold;
  font-size: 20px;
}

.appbtn {
  background: white;
  color: #009270;
  border: none;
  padding: 6px 10px;
  border-radius: 5px;
}

.content {
  padding: 12px;
}

.section-title {
  margin-bottom: 10px;
}

.card {
  background: white;
  padding: 12px;
  margin-bottom: 10px;
  border-radius: 6px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.card h4 {
  margin: 0 0 5px 0;
}

.card p {
  margin: 0;
  color: #444;
  font-size: 14px;
}

.bottom-nav {
  position: fixed;
  bottom: 0;
  width: 100%;
  background: white;
  display: flex;
  justify-content: space-around;
  padding: 8px 0;
  border-top: 1px solid #ccc;
  font-size: 14px;
}// 346
const API_KEY = "PASTE_YOUR_REAL_API_KEY_HERE";

const url = `https://api.cricapi.com/v1/currentMatches?apikey=${API_KEY}&offset=0`;

fetch(url)
  .then(res => res.json())
  .then(data => {
    let output = "";

    if (!data.data || data.data.length === 0) {
      output = "<p>No live matches now</p>";
    } else {
      data.data.forEach(match => {
        output += `
          <div class="card">
            <h4>${match.name}</h4>
            <p>${match.status}</p>
            <p><b>Format:</b> ${match.matchType}</p>
          </div>
        `;
      });
    }

    document.getElementById("matches").innerHTML = output;
  })
  .catch(() => {
    document.getElementById("matches").innerHTML =
      "<p>Failed to load live data</p>";
  });
