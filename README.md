<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Growing Flower</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
html,body{
  margin:0;
  padding:0;
  width:100%;
  height:100%;
  background:#000;
  overflow:hidden;
}
canvas{display:block;}
</style>
</head>

<body>
<canvas id="c"></canvas>

<script>
const canvas = document.getElementById("c");
const ctx = canvas.getContext("2d");

function resize(){
  canvas.width = innerWidth;
  canvas.height = innerHeight;
}
resize();
addEventListener("resize", resize);

let grow = 0;

function drawStem(x, y, len){
  ctx.strokeStyle = "#3cff6b";
  ctx.lineWidth = 6;
  ctx.beginPath();
  ctx.moveTo(x, y);
  ctx.lineTo(x, y - len);
  ctx.stroke();
}

function drawLeaf(x, y, dir){
  ctx.fillStyle = "#2ecc71";
  ctx.beginPath();
  ctx.ellipse(x + dir*18, y, 22, 10, dir, 0, Math.PI*2);
  ctx.fill();
}

function drawFlower(x, y, size){
  for(let i=0;i<6;i++){
    ctx.fillStyle = "#ffeb3b";
    ctx.beginPath();
    ctx.ellipse(
      x + Math.cos(i)*size,
      y + Math.sin(i)*size,
      size, size/2,
      i, 0, Math.PI*2
    );
    ctx.fill();
  }
  ctx.fillStyle="#ff9800";
  ctx.beginPath();
  ctx.arc(x,y,size/2,0,Math.PI*2);
  ctx.fill();
}

function animate(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  const baseX = canvas.width/2;
  const baseY = canvas.height*0.85;

  grow += 0.8;
  if(grow > 220) grow = 220;

  drawStem(baseX, baseY, grow);

  if(grow > 60) drawLeaf(baseX, baseY - 80, -1);
  if(grow > 110) drawLeaf(baseX, baseY - 140, 1);

  if(grow >= 220){
    drawFlower(baseX, baseY - 220, 20);
  }

  // floating particles
  for(let i=0;i<25;i++){
    ctx.fillStyle="rgba(255,255,255,0.03)";
    ctx.beginPath();
    ctx.arc(Math.random()*canvas.width,Math.random()*canvas.height,1,0,Math.PI*2);
    ctx.fill();
  }

  requestAnimationFrame(animate);
}

animate();
</script>
</body>
</html>
