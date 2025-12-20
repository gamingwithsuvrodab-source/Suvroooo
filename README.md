<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Demo Casino Site</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #0b0b0b;
    color: #fff;
}

header {
    background: #111;
    padding: 15px 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

header h1 {
    color: gold;
    margin: 0;
}

nav a {
    color: #fff;
    margin-left: 15px;
    text-decoration: none;
}

.banner {
    background: url('https://images.unsplash.com/photo-1604594849809-dfedbc827105') center/cover;
    padding: 80px 20px;
    text-align: center;
}

.banner h2 {
    font-size: 36px;
    color: gold;
}

.section {
    padding: 40px 20px;
}

.games {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
}

.game-card {
    background: #1c1c1c;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
}

.game-card h3 {
    color: gold;
}

.game-card button {
    padding: 10px 20px;
    border: none;
    background: gold;
    cursor: pointer;
    font-weight: bold;
}

.auth {
    max-width: 400px;
    margin: auto;
    background: #1c1c1c;
    padding: 20px;
    border-radius: 10px;
}

.auth input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
}

.auth button {
    width: 100%;
    padding: 10px;
    background: gold;
    border: none;
    font-weight: bold;
}

footer {
    background: #111;
    padding: 20px;
    text-align: center;
    font-size: 14px;
}
</style>
</head>

<body>

<header>
    <h1>ROYAL CASINO</h1>
    <nav>
        <a href="#">Home</a>
        <a href="#">Games</a>
        <a href="#">Login</a>
    </nav>
</header>

<div class="banner">
    <h2>Welcome Bonus 100%</h2>
    <p>Play Slots, Roulette & More</p>
</div>

<div class="section">
    <h2>Popular Games</h2>
    <div class="games">
        <div class="game-card">
            <h3>🎰 Slot Machine</h3>
            <p>Win big jackpots</p>
            <button onclick="playGame('Slot')">Play</button>
        </div>

        <div class="game-card">
            <h3>🎲 Roulette</h3>
            <p>Place your bets</p>
            <button onclick="playGame('Roulette')">Play</button>
        </div>

        <div class="game-card">
            <h3>🃏 Blackjack</h3>
            <p>Beat the dealer</p>
            <button onclick="playGame('Blackjack')">Play</button>
        </div>
    </div>
</div>

<div class="section">
    <h2>User Login</h2>
    <div class="auth">
        <input type="text" placeholder="Username">
        <input type="password" placeholder="Password">
        <button>Login</button>
    </div>
</div>

<footer>
    <p>⚠️ 18+ Only | Demo Casino Website</p>
    <p>© 2025 Royal Casino</p>
</footer>

<script>
function playGame(game) {
    alert(game + " game is demo only!");
}
</script>

</body>
</html>
