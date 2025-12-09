<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gamer Vibe Website</title>
<style>
  *{margin:0;padding:0;box-sizing:border-box;}
  
  html,body{
    width:100%;height:100%;
    font-family:'Orbitron',sans-serif;
    overflow:hidden;
    color:#fff;
    background:#000;
  }

  body{
    background-size:cover;
    background-position:center;
    background-repeat:no-repeat;
    transition:background-image 1s ease-in-out;
  }

  canvas#particleCanvas{
    position:fixed;
    top:0;left:0;
    width:100%;height:100%;
    z-index:0;
    pointer-events:none;
  }

  .overlay{
    position:fixed;
    top:0;left:0;
    width:100%;height:100%;
    background:rgba(0,0,0,0.3);
    z-index:1;
    pointer-events:none;
  }

  .slide{
    width:100%;height:100vh;
    display:none;
    padding:20px;
    overflow-y:auto;
    text-align:center;
    position:relative;
    z-index:2;
  }

  .active{display:block;animation:fadeIn 0.6s ease-in-out;}
  @keyframes fadeIn{from{opacity:0;transform:scale(1.05);}to{opacity:1;transform:scale(1);} }

  h1.title{
    font-size:2.2rem;
    margin-bottom:15px;
    color:#0ff;
    text-shadow:0 0 12px #0ff,0 0 20px #0ff;
  }

  h2{
    font-size:1.4rem;
    margin-bottom:12px;
    color:#0ff;
    text-shadow:0 0 8px #0ff;
  }

  p,label{font-size:1rem;margin:10px 0;color:#fff;}

  input,textarea,button,.link-button{
    width:95%;
    max-width:400px;
    margin:10px auto;
    padding:14px;
    font-size:1rem;
    border-radius:8px;
    border:1px solid #0ff;
    background-color:rgba(0,0,0,0.6);
    color:#fff;
    display:block;
    text-decoration:none;
  }

  button,.link-button{
    background:linear-gradient(90deg,#0ff,#00f);
    border:none;
    cursor:pointer;
    transition:transform 0.2s;
  }

  button:hover,.link-button:hover{
    transform:scale(1.05);
    background:linear-gradient(90deg,#00f,#0ff);
  }

  .card {
    margin:12px auto;
    max-width:450px;
    padding:15px;
    border:1px solid #0ff;
    background:rgba(0,0,0,0.5);
    border-radius:10px;
    box-shadow:0 0 12px #022;
  }

  .contact{
    margin-top:20px;
    font-size:0.9rem;
    color:#ccc;
  }

  .user-details{
    margin-top:20px;
    text-align:left;
    max-width:400px;
    margin-left:auto;
    margin-right:auto;
    background:rgba(0,0,0,0.6);
    padding:15px;
    border-radius:10px;
    border:1px solid #0ff;
  }

  #musicBtn{
    position:fixed;
    top:15px;right:15px;
    padding:10px 18px;
    border-radius:50px;
    font-size:0.9rem;
    z-index:10;
    text-shadow:0 0 8px #0ff;
  }
</style>
</head>
<body>

<!-- Neon Particle Canvas -->
<canvas id="particleCanvas"></canvas>
<div class="overlay"></div>

<!-- Music -->
<button id="musicBtn">🎵 Play Music</button>
<audio id="bgMusic" loop>
  <source src="https://www.bensound.com/bensound-music/bensound-epic.mp3" type="audio/mpeg">
</audio>

<!-- SLIDE 1 -->
<div class="slide active" id="slide1">
  <h1 class="title">WELCOME GAMER!</h1>
  <p>Press Start to Begin Your Journey 🎮</p>
  <button onclick="nextSlide()">▶ START</button>
</div>

<!-- SLIDE 2 -->
<div class="slide" id="slide2">
  <h1 class="title">ABOUT YOU</h1>
  <form id="gamerForm">
    <input type="text" name="name" placeholder="Your Name" required>
    <input type="text" id="usernameInput" name="username" placeholder="Gamer Username" required>
    <input type="text" name="game" placeholder="Favorite Game" required>
    <input type="text" name="level" placeholder="Your Level/Rank" required>
    <textarea name="bio" placeholder="Express Yourself..." rows="4" required></textarea>
    <button type="submit">Continue</button>
  </form>
</div>

<!-- SLIDE 3 -->
<div class="slide" id="slide3">
  <h1 class="title">NEED HELP?</h1>
  <label><input type="radio" name="needHelp" value="yes" onclick="toggleHelp(true)"> Yes</label>
  <label><input type="radio" name="needHelp" value="no" onclick="toggleHelp(false)"> No</label>
  <textarea id="helpText" placeholder="Describe your issue..." style="display:none;"></textarea>

  <div class="contact">📞 +91 96991 33348</div>
  <a class="link-button" id="whatsappBtn" target="_blank">💬 Message us on WhatsApp</a>

  <div class="user-details" id="userDetails"></div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 4 -->
<div class="slide" id="slide4">
  <h1 class="title">ROBLOX TIPS</h1>
  <div class="card">✔ Level up faster by doing daily quests</div>
  <div class="card">✔ Join groups for bonus XP</div>
  <div class="card">✔ Trade smart & avoid scammers</div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 5 -->
<div class="slide" id="slide5">
  <h1 class="title">ROBLOX CODES 🎁</h1>
  <div class="card">⭐ MEGA-BOOST-2025</div>
  <div class="card">⭐ FREE-COINS-777</div>
  <div class="card">⭐ XP-BOOSTER</div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 6 -->
<div class="slide" id="slide6">
  <h1 class="title">YOUR SUMMARY</h1>
  <p>Here is your saved profile:</p>
  <div class="user-details" id="summaryBox"></div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 7 -->
<div class="slide" id="slide7">
  <h1 class="title">POPULAR GAMES</h1>
  <div class="card">🔥 Blox Fruits</div>
  <div class="card">🔥 Arsenal</div>
  <div class="card">🔥 Brookhaven</div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 8 -->
<div class="slide" id="slide8">
  <h1 class="title">REVIEWS ⭐</h1>
  <div class="card">Arsenal – 9/10</div>
  <div class="card">Brookhaven – 8/10</div>
  <div class="card">Blox Fruits – 10/10</div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 9 -->
<div class="slide" id="slide9">
  <h1 class="title">GAMING NEWS ⚡</h1>
  <div class="card">• Roblox update coming soon...</div>
  <div class="card">• New anime games trending</div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 10 -->
<div class="slide" id="slide10">
  <h1 class="title">TOOLS</h1>
  <div class="card">🛠 DPS Calculator</div>
  <div class="card">🛠 XP Tool</div>
  <div class="card">🛠 Script Helper</div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 11 -->
<div class="slide" id="slide11">
  <h1 class="title">EXTRA TIPS</h1>
  <div class="card">✔ Play with friends for XP boost</div>
  <div class="card">✔ Set 2FA security</div>
  <button onclick="nextSlide()">Next ▶</button>
</div>

<!-- SLIDE 12 -->
<div class="slide" id="slide12">
  <h1 class="title">SUPPORT</h1>
  <a class="link-button" href="https://wa.me/919699133348">💬 Contact on WhatsApp</a>
  <button onclick="speak('Thanks for visiting Gamer Vibe!')">🔊 Thank You</button>
</div>

<script>
let currentSlide = 1;
const totalSlides = 12;

// Background slideshow
const wallpapers=[
  "https://wallpapercave.com/wp/wp5929128.jpg",
  "https://images.unsplash.com/photo-1511512578047-dfb367046420?auto=format&fit=crop&w=1600&q=80",
  "https://images.unsplash.com/photo-1632765743329-3b257fe779a6?auto=format&fit=crop&w=1600&q=80",
];
let index=0;
function changeBackground(){
  document.body.style.backgroundImage=`url('${wallpapers[index]}')`;
  index=(index+1)%wallpapers.length;
}
setInterval(changeBackground,3000);
changeBackground();

// Slide control
function nextSlide(){
  document.getElementById(`slide${currentSlide}`).classList.remove('active');
  currentSlide++;
  if(currentSlide>totalSlides)currentSlide=totalSlides;
  document.getElementById(`slide${currentSlide}`).classList.add('active');
}

// Help toggle
function toggleHelp(show){
  document.getElementById('helpText').style.display=show?'block':'none';
}

// Form + WhatsApp Integration
document.getElementById('gamerForm').addEventListener('submit',function(e){
  e.preventDefault();
  
  const formData=new FormData(this);
  const details=`Name: ${formData.get("name")}<br>
  Username: ${formData.get("username")}<br>
  Game: ${formData.get("game")}<br>
  Level: ${formData.get("level")}<br>
  Bio: ${formData.get("bio")}`;
  
  document.getElementById('userDetails').innerHTML=details;
  document.getElementById('summaryBox').innerHTML=details;

  nextSlide();
});

// Music control
const musicBtn=document.getElementById('musicBtn');
const bgMusic=document.getElementById('bgMusic');
let isPlaying=false;
musicBtn.addEventListener('click',()=>{
  if(isPlaying){bgMusic.pause();musicBtn.textContent="🎵 Play Music";}
  else{bgMusic.play();musicBtn.textContent="⏸ Pause Music";}
  isPlaying=!isPlaying;
});

// Voice assistant
function speak(t){
  if("speechSynthesis" in window){
    let u=new SpeechSynthesisUtterance(t);
    speechSynthesis.cancel();
    speechSynthesis.speak(u);
  }
}

// Particles
const canvas=document.getElementById('particleCanvas');
const ctx=canvas.getContext('2d');
function resize(){canvas.width=innerWidth;canvas.height=innerHeight;}
resize(); addEventListener('resize',resize);

const particles=[];
for(let i=0;i<120;i++){
  particles.push({
    x:Math.random()*canvas.width,
    y:Math.random()*canvas.height,
    vx:(Math.random()-0.5)*0.8,
    vy:(Math.random()-0.5)*0.8,
    size:Math.random()*3+1,
    hue:Math.random()*360
  });
}

function drawParticles(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  particles.forEach(p=>{
    p.x+=p.vx; p.y+=p.vy;
    if(p.x<0||p.x>canvas.width)p.vx*=-1;
    if(p.y<0||p.y>canvas.height)p.vy*=-1;
    p.hue+=0.5;

    ctx.beginPath();
    ctx.shadowColor=`hsl(${p.hue},100%,60%)`;
    ctx.shadowBlur=12;
    ctx.fillStyle=`hsl(${p.hue},100%,60%)`;
    ctx.arc(p.x,p.y,p.size,0,Math.PI*2);
    ctx.fill();
  });
  requestAnimationFrame(drawParticles);
}
drawParticles();
</script>
</body>
</html>
