<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Pomodoro Focus</title>
<style>
body{font-family:Arial;background:#eff6ff;display:grid;place-items:center;min-height:100vh;margin:0}
main{background:white;padding:30px;border-radius:18px;text-align:center;width:min(90%,420px);box-shadow:0 8px 30px #0001}
h1{color:#1d4ed8}
#timer{font-size:65px;font-weight:bold;margin:25px}
button{padding:12px 20px;border:0;border-radius:8px;background:#2563eb;color:white;cursor:pointer;margin:5px}
button.secondary{background:#64748b}
</style>
</head>
<body>
<main>
<h1>Pomodoro Focus</h1>
<p>Stay focused and manage your time.</p>
<div id="timer">25:00</div>
<button onclick="startTimer()">Start / Resume</button>
<button class="secondary" onclick="pauseTimer()">Pause</button>
<button class="secondary" onclick="resetTimer()">Reset</button>
<p id="status">Ready to focus!</p>
</main>
<script>
let remaining=1500;
let interval=null;
const timer=document.getElementById("timer");
const status=document.getElementById("status");

function render(){
 const m=Math.floor(remaining/60);
 const s=remaining%60;
 timer.textContent=String(m).padStart(2,"0")+":"+String(s).padStart(2,"0");
}
function startTimer(){
 if(interval||remaining<=0)return;
 status.textContent="Focus session running";
 interval=setInterval(()=>{
  remaining--;
  render();
  if(remaining<=0){
   pauseTimer();
   status.textContent="Session completed! Great work.";
   alert("Focus session completed!");
  }
 },1000);
}
function pauseTimer(){
 clearInterval(interval);
 interval=null;
 if(remaining>0)status.textContent="Timer paused";
}
function resetTimer(){
 pauseTimer();
 remaining=1500;
 render();
 status.textContent="Timer reset. Ready to focus!";
}
render();
</script>
</body>
</html>
