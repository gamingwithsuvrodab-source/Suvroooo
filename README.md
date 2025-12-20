<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>I Love You ❤️</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

body{
  width:100vw;
  height:100vh;
  background:linear-gradient(180deg,#0a0015,#1a002a,#000);
  display:flex;
  justify-content:center;
  align-items:center;
  overflow:hidden;
  font-family:'Poppins',sans-serif;
}

.reel{
  width:100%;
  max-width:420px;
  height:100vh;
  position:relative;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
}

.heart-box{
  position:relative;
  width:260px;
  height:240px;
}

.heart{
  position:absolute;
  width:14px;
  height:14px;
  background:red;
  transform:rotate(45deg);
  animation:pulse 1.4s infinite;
}

.heart::before,
.heart::after{
  content:"";
  position:absolute;
  width:14px;
  height:14px;
  background:inherit;
  border-radius:50%;
}

.heart::before{top:-7px;left:0;}
.heart::after{left:-7px;top:0;}

@keyframes pulse{
  0%{transform:scale(1) rotate(45deg);}
  50%{transform:scale(1.5) rotate(45deg);}
  100%{transform:scale(1) rotate(45deg);}
}

h1{
  margin-top:25px;
  font-size:40px;
  color:#ff2d75;
  animation:glow 2s infinite alternate, slideUp 1.5s ease;
}

@keyframes glow{
  from{text-shadow:0 0 10px #ff2d75;}
  to{text-shadow:0 0 30px #ff69b4;}
}

@keyframes slideUp{
  from{opacity:0;transform:translateY(40px);}
  to{opacity:1;transform:translateY(0);}
}

/* floating background hearts */
.float-heart{
  position:absolute;
  bottom:-30px;
  width:18px;
  height:18px;
  background:red;
  transform:rotate(45deg);
  animation:rise linear infinite;
}

.float-heart::before,
.float-heart::after{
  content:"";
  position:absolute;
  width:18px;
  height:18px;
  background:inherit;
  border-radius:50%;
}

.float-heart::before{top:-9px;left:0;}
.float-heart::after{left:-9px;top:0;}

@keyframes rise{
  from{transform:translateY(0) rotate(45deg);opacity:1;}
  to{transform:translateY(-120vh) rotate(45deg);opacity:0;}
}

.footer{
  position:absolute;
  bottom:40px;
  color:#fff;
  opacity:.7;
  font-size:14px;
}
</style>
</head>

<body>

<div class="reel">
  <div class="heart-box" id="heartBox"></div>
  <h1>I Love You ❤️</h1>
  <div class="footer">For You 💖</div>
</div>

<script>
const points=[
[130,20],[115,35],[95,55],[75,75],[65,95],[70,120],
[90,145],[110,165],[130,185],[150,165],[170,145],
[190,120],[195,95],[185,75],[165,55],[145,35]
];

const colors=["#ff0033","#ff2d75","#ff69b4","#ff1493"];

points.forEach((p,i)=>{
  const h=document.createElement("div");
  h.className="heart";
  h.style.left=p[0]+"px";
  h.style.top=p[1]+"px";
  h.style.background=colors[i%colors.length];
  document.getElementById("heartBox").appendChild(h);
});

// Floating hearts
setInterval(()=>{
  const f=document.createElement("div");
  f.className="float-heart";
  f.style.left=Math.random()*100+"vw";
  f.style.background=colors[Math.floor(Math.random()*colors.length)];
  f.style.animationDuration=3+Math.random()*4+"s";
  document.body.appendChild(f);
  setTimeout(()=>f.remove(),7000);
},300);
</script>

</body>
</html><body>

<audio id="bgMusic" loop>
  <source src="song.mp3" type="audio/mpeg">
</audio>

<div class="reel">
  <!-- 

https://github.com/user-attachments/assets/63295bc5-5133-42d5-8bc4-a9e710d29a62

 -->
</div>

</body>
