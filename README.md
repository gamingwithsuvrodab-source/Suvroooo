<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>I Love You ❤️</title>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

body{
  height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
  background:linear-gradient(135deg,#000,#2c003e);
  overflow:hidden;
  font-family:'Georgia', serif;
}

.card{
  background:#fff;
  padding:30px;
  border-radius:25px;
  text-align:center;
  box-shadow:0 0 40px rgba(255,0,100,.5);
}

.heart-container{
  position:relative;
  width:300px;
  height:260px;
  margin:auto;
}

.heart{
  position:absolute;
  width:16px;
  height:16px;
  background:red;
  transform:rotate(45deg);
  animation:pulse 1.5s infinite, float 4s infinite;
}

.heart::before,
.heart::after{
  content:"";
  position:absolute;
  width:16px;
  height:16px;
  background:inherit;
  border-radius:50%;
}

.heart::before{ top:-8px; left:0; }
.heart::after{ left:-8px; top:0; }

@keyframes pulse{
  0%{transform:scale(1) rotate(45deg);}
  50%{transform:scale(1.4) rotate(45deg);}
  100%{transform:scale(1) rotate(45deg);}
}

@keyframes float{
  0%{opacity:0.7;}
  50%{opacity:1;}
  100%{opacity:0.7;}
}

h1{
  margin-top:20px;
  font-size:36px;
  animation:textGlow 2s infinite alternate;
}

@keyframes textGlow{
  from{
    color:#ff004c;
    text-shadow:0 0 10px #ff004c;
  }
  to{
    color:#ff69b4;
    text-shadow:0 0 25px #ff69b4;
  }
}

/* Floating hearts background */
.bg-heart{
  position:absolute;
  bottom:-20px;
  width:20px;
  height:20px;
  background:red;
  transform:rotate(45deg);
  animation:rise 6s linear infinite;
}

.bg-heart::before,
.bg-heart::after{
  content:"";
  position:absolute;
  width:20px;
  height:20px;
  background:inherit;
  border-radius:50%;
}

.bg-heart::before{ top:-10px; left:0;}
.bg-heart::after{ left:-10px; top:0;}

@keyframes rise{
  0%{transform:translateY(0) rotate(45deg); opacity:1;}
  100%{transform:translateY(-120vh) rotate(45deg); opacity:0;}
}

@media(max-width:480px){
  .heart-container{ width:240px; height:220px; }
  h1{ font-size:28px; }
}
</style>
</head>

<body>

<div class="card">
  <div class="heart-container" id="heartBox"></div>
  <h1>I Love You ❤️</h1>
</div>

<script>
// Heart shape points
const points=[
[150,20],[130,35],[110,55],[90,75],[80,95],[85,120],
[100,145],[120,165],[150,190],[180,165],[200,145],
[215,120],[220,95],[210,75],[190,55],[170,35]
];

const colors=["#ff004c","#ff1493","#ff69b4","#e60073"];

points.forEach((p,i)=>{
  const h=document.createElement("div");
  h.className="heart";
  h.style.left=p[0]+"px";
  h.style.top=p[1]+"px";
  h.style.background=colors[i%colors.length];
  document.getElementById("heartBox").appendChild(h);
});

// Floating background hearts
setInterval(()=>{
  const bg=document.createElement("div");
  bg.className="bg-heart";
  bg.style.left=Math.random()*100+"vw";
  bg.style.background=colors[Math.floor(Math.random()*colors.length)];
  bg.style.animationDuration=4+Math.random()*4+"s";
  document.body.appendChild(bg);
  setTimeout(()=>bg.remove(),8000);
},400);
</script>

</body>
</html>

