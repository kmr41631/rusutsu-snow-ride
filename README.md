# rusutsu-snow-ride
ルスツスノーボードゲーム
<!DOCTYPE html>

<html lang="ja">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=no">

<title>RUSUTSU SNOW RIDE</title>

<style>

*{

  box-sizing:border-box;

  -webkit-user-select:none;

  user-select:none;

}

body{

  margin:0;

  overflow:hidden;

  background:#111;

  font-family:Arial,sans-serif;

}

#game{

  position:relative;

  width:100vw;

  height:100vh;

  overflow:hidden;

  background:linear-gradient(#72b9e8 0%,#dff5ff 38%,#b9d4df 100%);

}

#mountain{

  position:absolute;

  top:13%;

  left:-10%;

  width:120%;

  height:32%;

  background:#7896a5;

  clip-path:polygon(

    0 100%,12% 55%,22% 75%,34% 25%,

    45% 65%,58% 10%,70% 58%,83% 30%,

    100% 75%,100% 100%

  );

  opacity:.75;

}

#snow{

  position:absolute;

  bottom:-8%;

  left:-15%;

  width:130%;

  height:82%;

  background:white;

  clip-path:polygon(

    35% 0,65% 0,78% 10%,88% 28%,

    100% 100%,0 100%,12% 30%,22% 10%

  );

  transform:rotate(1deg);

}

.tree{

  position:absolute;

  width:0;

  height:0;

  border-left:22px solid transparent;

  border-right:22px solid transparent;

  border-bottom:75px solid #315a4a;

}

.tree:after{

  content:"";

  position:absolute;

  left:-17px;

  top:35px;

  border-left:17px solid transparent;

  border-right:17px solid transparent;

  border-bottom:60px solid #315a4a;

}

.t1{left:5%;bottom:25%}

.t2{right:7%;bottom:30%;transform:scale(.8)}

.t3{left:15%;bottom:40%;transform:scale(.55)}

.t4{right:18%;bottom:43%;transform:scale(.65)}

#course{

  position:absolute;

  left:50%;

  top:-10%;

  width:76%;

  height:120%;

  transform:translateX(-50%);

  background:#f8fbfc;

  clip-path:polygon(

    39% 0,61% 0,67% 15%,60% 30%,

    72% 45%,58% 62%,70% 78%,

    55% 100%,45% 100%,30% 78%,

    42% 62%,28% 45%,40% 30%,33% 15%

  );

  box-shadow:0 0 25px rgba(0,0,0,.15);

}

#course:after{

  content:"";

  position:absolute;

  inset:0;

  background:repeating-linear-gradient(

    110deg,

    transparent 0,

    transparent 80px,

    rgba(150,180,190,.15) 82px,

    transparent 84px

  );

}

#player{

  position:absolute;

  left:50%;

  bottom:17%;

  transform:translateX(-50%);

  font-size:54px;

  z-index:10;

  transition:transform .15s;

}

#hud{

  position:absolute;

  top:15px;

  left:15px;

  right:15px;

  z-index:20;

  display:flex;

  justify-content:space-between;

  gap:8px;

}

.box{

  background:rgba(0,0,0,.65);

  color:white;

  padding:9px 12px;

  border-radius:12px;

  font-weight:bold;

  font-size:13px;

}

#buttons{

  position:absolute;

  bottom:25px;

  left:0;

  right:0;

  z-index:30;

  display:flex;

  justify-content:center;

  gap:30px;

}

.turn{

  width:75px;

  height:75px;

  border-radius:50%;

  border:2px solid white;

  background:rgba(0,0,0,.55);

  color:white;

  font-size:35px;

}

.turn:active{

  background:rgba(255,255,255,.4);

}

#start,

#finish{

  position:absolute;

  inset:0;

  z-index:100;

  background:rgba(0,0,0,.72);

  color:white;

  display:flex;

  flex-direction:column;

  justify-content:center;

  align-items:center;

  text-align:center;

  padding:25px;

}

#finish{

  display:none;

}

h1{

  margin:0 0 10px;

  font-size:32px;

}

h2{

  margin:8px 0;

}

p{

  line-height:1.6;

}

.mainBtn{

  margin-top:20px;

  padding:15px 35px;

  border:0;

  border-radius:30px;

  background:white;

  color:#222;

  font-size:18px;

  font-weight:bold;

}

#progress{

  position:absolute;

  top:75px;

  left:15px;

  right:15px;

  height:7px;

  background:rgba(0,0,0,.25);

  border-radius:10px;

  overflow:hidden;

  z-index:20;

}

#bar{

  width:0%;

  height:100%;

  background:white;

}

</style>

</head>

<body>

<div id="game">

  <div id="mountain"></div>

  <div class="tree t1"></div>

  <div class="tree t2"></div>

  <div class="tree t3"></div>

  <div class="tree t4"></div>

  <div id="snow"></div>

  <div id="course"></div>

  <div id="hud">

    <div class="box">🏔️ ISOLA GRAND</div>

    <div class="box">📏 <span id="distance">3500</span>m</div>

    <div class="box">⚡ <span id="speed">0</span> km/h</div>

  </div>

  <div id="progress">

    <div id="bar"></div>

  </div>

  <div id="player">🏂</div>

  <div id="buttons">

    <button class="turn" id="left">←</button>

    <button class="turn" id="right">→</button>

  </div>

  <div id="start">

    <h1>RUSUTSU<br>SNOW RIDE</h1>

    <h2>ISOLA GRAND</h2>

    <p>

      ルスツ・イゾラグランドを滑ろう！<br>

      左右ボタンでターンしてゴールを目指せ！

    </p>

    <p>

      📏 約3,500m<br>

      📐 平均12°<br>

      🔥 最大20°<br>

      ⭐ 中級

    </p>

    <button class="mainBtn" onclick="startGame()">START</button>

  </div>

  <div id="finish">

    <h1>🏁 FINISH!</h1>

    <h2>ISOLA GRAND</h2>

    <p id="result"></p>

    <button class="mainBtn" onclick="location.reload()">もう一度滑る</button>

  </div>

</div>

<script>

let distance = 3500;

let speed = 0;

let position = 0;

let startTime;

let gameRunning = false;

let timer;

const player = document.getElementById("player");

const distanceText = document.getElementById("distance");

const speedText = document.getElementById("speed");

const bar = document.getElementById("bar");

function startGame(){

  document.getElementById("start").style.display="none";

  gameRunning=true;

  startTime=Date.now();

  speed=35;

  timer=setInterval(updateGame,100);

}

function updateGame(){

  if(!gameRunning) return;

  distance -= speed * 0.1;

  if(distance < 0){

    distance=0;

  }

  distanceText.textContent=Math.floor(distance);

  speedText.textContent=Math.floor(speed);

  let progress=(3500-distance)/3500*100;

  bar.style.width=progress+"%";

  if(distance<=0){

    finishGame();

  }

}

function turn(direction){

  if(!gameRunning) return;

  position += direction * 18;

  if(position>115) position=115;

  if(position<-115) position=-115;

  player.style.transform=

    "translateX(calc(-50% + "+position+"px)) rotate("+

    (direction*18)+"deg)";

  speed += 4;

  if(speed>65) speed=65;

  setTimeout(()=>{

    player.style.transform=

      "translateX(calc(-50% + "+position+"px)) rotate(0deg)";

  },180);

}

document.getElementById("left").addEventListener(

  "touchstart",

  function(e){

    e.preventDefault();

    turn(-1);

  }

);

document.getElementById("right").addEventListener(

  "touchstart",

  function(e){

    e.preventDefault();

    turn(1);

  }

);

document.getElementById("left").addEventListener(

  "click",

  ()=>turn(-1)

);

document.getElementById("right").addEventListener(

  "click",

  ()=>turn(1)

);

let touchStartX=0;

document.addEventListener("touchstart",e=>{

  touchStartX=e.touches[0].clientX;

});

document.addEventListener("touchend",e=>{

  if(!gameRunning) return;

  let endX=e.changedTouches[0].clientX;

  let diff=endX-touchStartX;

  if(Math.abs(diff)>40){

    if(diff>0){

      turn(1);

    }else{

      turn(-1);

    }

  }

});

function finishGame(){

  gameRunning=false;

  clearInterval(timer);

  let time=((Date.now()-startTime)/1000).toFixed(1);

  document.getElementById("finish").style.display="flex";

  document.getElementById("result").innerHTML=

    "滑走タイム：<strong>"+time+"秒</strong><br><br>"+

    "🏂 お疲れさま！";

}

</script>

</body>

</html>
