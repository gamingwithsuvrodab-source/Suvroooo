<audio id="bgMusic" loop>
  <source src="song.mp3" type="audio/mpeg">
</audio>

<button id="playBtn">▶ TAP TO PLAY</button>

https://github.com/user-attachments/assets/feac3177-a466-4807-94f5-2927a32c7af9
#playBtn{
  position:fixed;
  top:50%;
  left:50%;
  transform:translate(-50%,-50%);
  padding:15px 30px;
  font-size:18px;
  border:none;
  border-radius:30px;
  background:#ff2d75;
  color:#fff;
  z-index:9999;
}<script>
const music = document.getElementById("bgMusic");
const btn = document.getElementById("playBtn");

btn.addEventListener("click", () => {
  music.volume = 0.8;
  music.play();
  btn.style.display = "none"; // button hide
});
</script>
  
