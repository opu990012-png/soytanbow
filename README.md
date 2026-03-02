<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday My Love ❤️</title>
<style>
body{
margin:0;
font-family:'Segoe UI',sans-serif;
background:#ffe6eb;
color:#ff4d6d;
overflow-x:hidden;
}
.page{
display:none;
height:100vh;
justify-content:center;
align-items:center;
flex-direction:column;
position:relative;
text-align:center;
padding:10px;
}
.active{ display:flex; }

/* Left & Right stacked */
.left, .right{
width:100%;
text-align:center;
margin-bottom:15px;
}
.left h1{
font-size:32px;
text-shadow:2px 2px 10px white;
margin-bottom:10px;
}
.subtitle{
font-size:16px;
color:#444;
margin-bottom:15px;
}

/* Buttons */
button{
padding:12px 25px;
border:none;
border-radius:25px;
background:#ff4d6d;
color:white;
cursor:pointer;
margin:8px;
box-shadow:0 4px 10px rgba(0,0,0,0.2);
font-size:16px;
}

/* Images */
.circle-img{
width:220px;
height:220px;
border-radius:50%;
object-fit:cover;
border:6px solid #ff4d6d;
box-shadow:0 0 25px #ff4d6d;
margin-bottom:15px;
}

/* Float animation */
.float{
position:absolute;
font-size:30px;
animation:float 3s infinite ease-in-out;
}
@keyframes float{
0%{transform:translateY(0);}
50%{transform:translateY(-20px);}
100%{transform:translateY(0);}
}

/* Modal */
.modal{
position:fixed;
top:0;left:0;
width:100%;height:100%;
background:rgba(0,0,0,0.6);
display:none;
justify-content:center;
align-items:center;
}
.modal-content{
background:white;
padding:25px;
width:90%;
max-width:500px;
border-radius:15px;
max-height:80vh;
overflow:auto;
}
#wishText{white-space:pre-line; color:#333;}

/* Gift Boxes */
.photo-grid{
display:grid;
grid-template-columns:repeat(2,180px);
gap:20px;
justify-content:center;
}
.photo-box{
width:180px;
height:180px;
background:#ff4d6d;
display:flex;
justify-content:center;
align-items:center;
border-radius:15px;
font-size:50px;
cursor:pointer;
}

/* Game */
#gameArea{
position:relative;
width:100%;
height:60vh;
overflow:hidden;
}
.balloon{
position:absolute;
bottom:-60px;
cursor:pointer;
}

/* Congrats */
#pageCongrats h1{
font-size:36px;
color:gold;
text-shadow:0 0 20px yellow;
margin-bottom:15px;
}
#pageCongrats p{
font-size:18px;
margin-bottom:15px;
}

/* Gallery images */
#pageGallery img{
width:140px;
margin:5px;
border-radius:10px;
}
#finalPhoto{
display:none;
width:200px;
margin-top:15px;
border-radius:10px;
}
</style>
</head>
<body>

<!-- Background Music -->
<audio id="bgMusic" loop>
<source src="love.mp3" type="audio/mpeg">
</audio>

<!-- PAGE 1 -->
<div class="page active" id="page1">
  <div class="left">
    <h1>🎉 Happy Birthday My Love</h1>
    <div class="subtitle">You are the most special person in my life 💕</div>
    <button onclick="startMusic();openModal()">Click for Surprise 💌</button>
  </div>
  <div class="right">
    <img src="gf.jpg" class="circle-img">
    <div class="float" style="top:5%;left:5%;">🎈</div>
    <div class="float" style="top:15%;right:10%;">❤️</div>
    <div class="float" style="bottom:10%;left:20%;">🎈</div>
  </div>
</div>

<!-- MODAL -->
<div class="modal" id="modal">
<div class="modal-content">
<h3>To My Love ❤️</h3>
<div id="wishText"></div>
<br>
<button onclick="goPage2()">Next</button>
</div>
</div>

<!-- PAGE 2 -->
<div class="page" id="page2">
<h2>DO YOU LOVE ME ❤️</h2>
<button onclick="goLove()">YES 💕</button>
<button id="noBtn" onmouseover="moveNo()">NO 😒</button>
</div>

<!-- PAGE 3 -->
<div class="page" id="pageLove">
<h1 id="loveText" style="font-size:36px;"></h1>
<button onclick="switchPage('pageGift')">Next 💌</button>
</div>

<!-- PAGE 4 -->
<div class="page" id="pageGift">
<h2>Select One 🎁</h2>
<button onclick="giftWarning()">Gift 🎁</button>
<button onclick="switchPage('pageMemory')">Memory 💖</button>
<p id="warning" style="color:red;"></p>
</div>

<!-- PAGE 5 -->
<div class="page" id="pageMemory">
<h2>Tap To Unlock 🔒</h2>
<div class="photo-grid">
<div class="photo-box" onclick="startGame()">🔒</div>
<div class="photo-box" onclick="startGame()">🔒</div>
<div class="photo-box" onclick="startGame()">🔒</div>
<div class="photo-box" onclick="startGame()">🔒</div>
</div>
</div>

<!-- PAGE 6 GAME -->
<div class="page" id="pageGame">
<h2>Pop 5 Balloons 🎈</h2>
<div id="gameArea"></div>
<p id="score">0 / 5</p>
</div>

<!-- PAGE 7 CONGRATS -->
<div class="page" id="pageCongrats">
<h1>CONGRATULATIONS ✨</h1>
<p>রুপা বউ তুমি পেরেছো 💖</p>
<button onclick="switchPage('pageGallery')">See Photos</button>
</div>

<!-- PAGE 8 GALLERY -->
<div class="page" id="pageGallery">
<h2>Our Beautiful Memories ❤️</h2>
<img src="memory1.jpg">
<img src="memory2.jpg"><br>
<img src="memory3.jpg">
<img src="memory4.jpg">
<br>
<button onclick="showFinalGift()">Open Final Gift 🎁</button>
<img src="photo.jpg" id="finalPhoto">
</div>

<script>
/* MUSIC */
function startMusic(){
let music=document.getElementById("bgMusic");
music.volume=0.5;
music.play().catch(e=>{alert("Tap the button to play music 🎵");});
}

/* PAGE SWITCH */
function switchPage(id){
document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

/* WISH LETTER */
var text=`প্রিয় জান,  
  
শুভ জন্মদিন আমার ভালোবাসা। 🎂💖  
আজকের এই বিশেষ দিনে আমি শুধু একটা কথাই বলতে চাই — তুমি আমার জীবনের সবচেয়ে সুন্দর প্রাপ্তি। তিন বছরেরও বেশি সময় ধরে আমরা একসাথে আছি। এই সময়টায় রাগ ছিল, অভিমান ছিল, ভুল বোঝাবুঝি ছিল… কিন্তু সব কিছুর মাঝেও আমাদের ভালোবাসাটা কখনো কমে যায়নি। বরং আরও গভীর হয়েছে।  
  
আমি জানি, এতদিনে তোমাকে ঠিকভাবে বড় কোনো গিফট দিতে পারিনি। তোমার প্রাপ্যটা সবসময় দিতে পারিনি। কিন্তু বিশ্বাস করো, আমার মন থেকে তোমার জন্য ভালোবাসা আর সম্মান কখনো কম ছিল না। আমার সামর্থ্য যতটুকু, তার চেয়েও বেশি ভালোবাসা আমি তোমাকে দিতে চাই।  
  
আমাদের সম্পর্কটা শুধু আজকের না — এটা আমাদের ভবিষ্যতেরও। আমি চাই আমরা একসাথে পূর্ণতা পাই, একসাথে স্বপ্ন দেখি, একসাথে সব রাগ-অভিমান পেরিয়ে জীবনের প্রতিটা মুহূর্ত কাটাই।  
  
তুমি আমার শান্তি, তুমি আমার হাসি, তুমি আমার ভরসা। তোমার হাতটা যেন কোনোদিন না ছুটে যায়।  
  
আল্লাহর কাছে শুধু এই দোয়া করি — তোমার জীবন সুখে, স্বাস্থ্যে আর সফলতায় ভরে উঠুক। আর সেই সুখের প্রতিটা মুহূর্তে যেন আমি তোমার পাশে থাকতে পারি।  
  
শুভ জন্মদিন আমার জান।  
অনেক অনেক ভালোবাসা রইলো তোমার জন্য। ❤️  
  
তোমার জামাই 💕`;
var i=0;
function openModal(){
document.getElementById("wishText").innerHTML="";
i=0;
document.getElementById("modal").style.display="flex";
typeWriter();
}
function typeWriter(){
if(i<text.length){
document.getElementById("wishText").innerHTML+=text.charAt(i);
i++;
setTimeout(typeWriter,20);
}
}
function goPage2(){
document.getElementById("modal").style.display="none";
switchPage("page2");
}

/* NO BUTTON MOVE */
function moveNo(){
let btn=document.getElementById("noBtn");
btn.style.position="absolute";
btn.style.top=Math.random()*70+"%";
btn.style.left=Math.random()*70+"%";
}

/* LOVE TEXT */
function goLove(){
switchPage("pageLove");
let msg="I LOVE YOU ❤️";
let j=0;
let target=document.getElementById("loveText");
target.innerHTML="";
let inter=setInterval(()=>{
if(j<msg.length){
target.innerHTML+=msg[j]; j++;
}else clearInterval(inter);
},150);
}

/* GIFT WARNING */
function giftWarning(){
document.getElementById("warning").innerText="⚠ আগে Memory দেখো!";
}

/* GAME */
let score=0;
let interval;
function startGame(){
switchPage("pageGame");
score=0;
document.getElementById("score").innerText="0 / 5";
document.getElementById("gameArea").innerHTML="";
interval=setInterval(createBalloon,800);
}
function createBalloon(){
let colors=["red","pink","blue","yellow"];
let b=document.createElement("div");
b.className="balloon";
b.style.color=colors[Math.floor(Math.random()*colors.length)];
b.style.fontSize=(60+Math.random()*10)+"px"; // 60-70px
b.innerHTML="🎈";
b.style.left=Math.random()*80+"%";
b.onclick=function(){b.remove(); score++; document.getElementById("score").innerText=score+" / 5"; if(score>=5){clearInterval(interval);switchPage("pageCongrats");}};
document.getElementById("gameArea").appendChild(b);
let move=setInterval(()=>{
b.style.bottom=parseInt(b.style.bottom||-60)+3+"px";
if(parseInt(b.style.bottom)>500){b.remove(); clearInterval(move);}
},20);
}

/* FINAL GIFT */
function showFinalGift(){
document.getElementById("finalPhoto").style.display="block";
}
</script>
</body>
</html>
