<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Glowing Heart</title>
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
canvas{
  display:block;
}
</style>
</head>

<body>

<canvas id="c"></canvas>

<script>
const canvas = document.getElementById("c");
const ctx = canvas.getContext("2d");

function resize(){
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resize();
window.addEventListener("resize", resize);

let t = 0;

function heart(t, scale){
  const x = scale * 16 * Math.pow(Math.sin(t),3);
  const y = -scale * (
    13*Math.cos(t) -
    5*Math.cos(2*t) -
    2*Math.cos(3*t) -
    Math.cos(4*t)
  );
  return {x,y};
}

function draw(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  ctx.save();
  ctx.translate(canvas.width/2, canvas.height/2);

  for(let s=6; s<18; s++){
    ctx.beginPath();
    for(let i=0;i<Math.PI*2;i+=0.02){
      const p = heart(i+t*0.4, s*4);
      ctx.lineTo(p.x,p.y);
    }
    ctx.closePath();
    ctx.strokeStyle = `rgba(255,0,60,${0.15 + s*0.02})`;
    ctx.lineWidth = 1.5;
    ctx.stroke();
  }

  ctx.restore();
  t += 0.01;
  requestAnimationFrame(draw);
}

draw();
</script>

</body>
</html>
