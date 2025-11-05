<!doctype html>
<html lang="vi">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>GibThu — Tối nay khó ngủ quá</title>
<style>
  :root{
    --bg:#0f0b14;
    --panel:#191021;
    --accent:#ff6b9f;
    --muted: #bdb2c5;
  }
  html,body{height:100%;margin:0;font-family: "Segoe UI", Roboto, "Helvetica Neue", Arial;}
  body{
    background: radial-gradient(ellipse at top left, rgba(255,107,159,0.08), transparent 10%),
                linear-gradient(180deg,var(--bg),#07050a 70%);
    color:#fff;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:24px;
  }
  .card{
    width:min(520px, 95%);
    background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01));
    border-radius:18px;
    padding:28px;
    box-shadow: 0 8px 30px rgba(0,0,0,0.6), 0 1px 0 rgba(255,255,255,0.02) inset;
    position:relative;
    overflow:hidden;
    border: 1px solid rgba(255,255,255,0.03);
  }
  h1{
    margin:0 0 12px 0;
    font-size:20px;
    letter-spacing:0.2px;
    color:var(--accent);
    text-shadow: 0 2px 14px rgba(255,107,159,0.12);
  }
  p.lead{
    margin:0 0 18px 0;
    color:var(--muted);
    font-size:16px;
  }
  .choices{
    display:flex;
    gap:12px;
    margin-bottom:18px;
  }
  button.choice{
    flex:1;
    padding:12px 16px;
    border-radius:10px;
    border:0;
    cursor:pointer;
    font-weight:600;
    background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    color:#fff;
    transition:transform .12s ease, box-shadow .12s ease, opacity .12s;
    box-shadow: 0 6px 18px rgba(0,0,0,0.45);
  }
  button.choice:active{transform:translateY(1px) scale(.997);}
  button.choice:hover{box-shadow: 0 10px 24px rgba(0,0,0,0.55);}
  button#yes{background: linear-gradient(180deg,#ff6b9f,#ff4f88);}
  button#no{background: linear-gradient(180deg,#444,#333); color:#ddd;}
  .result{
    min-height:62px;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:20px;
    font-weight:700;
    color:#fff;
    opacity:0;
    transform:translateY(6px) scale(.99);
    transition:all .35s cubic-bezier(.2,.9,.25,1);
    text-align:center;
    padding:12px;
    border-radius:10px;
    background: linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    box-shadow: inset 0 -3px 10px rgba(0,0,0,0.2);
  }
  .result.show{opacity:1; transform:translateY(0) scale(1);}
  /* heart animations */
  .hearts {
    pointer-events:none;
    position:absolute;
    inset:0;
    z-index:5;
  }
  .heart {
    position:absolute;
    width:26px;
    height:26px;
    transform:translate(-50%,-50%) scale(.8);
    opacity:0;
    animation:floatUp linear;
  }
  .heart::before, .heart::after {
    content:"";
    position:absolute;
    left:50%;
    top:0;
    width:13px;height:20px;
    background:var(--accent);
    border-radius:12px 12px 0 0;
    transform-origin:50% 100%;
  }
  .heart::before { transform:translateX(-12px) rotate(-45deg); }
  .heart::after  { transform:translateX(-1px) rotate(45deg); }
  @keyframes floatUp {
    0% { opacity:0; transform:translate(-50%,0) scale(.6) translateY(0) rotate(0deg); }
    10% { opacity:1; }
    100% { opacity:0; transform:translate(-50%,-600px) scale(1.2) translateY(-600px) rotate(25deg); }
  }
  /* soft glow */
  .glow {
    position:absolute;
    left:50%;
    top:20%;
    width:360px;
    height:360px;
    transform:translateX(-50%);
    filter: blur(34px);
    opacity:0.12;
    pointer-events:none;
    z-index:1;
    background: radial-gradient(circle at 30% 30%, rgba(255,107,159,0.35), transparent 20%),
                radial-gradient(circle at 70% 70%, rgba(84,88,255,0.16), transparent 20%);
  }
  /* small sparkle */
  .sparkle {
    position:absolute;
    width:6px;height:6px;
    border-radius:50%;
    background:#fff;
    opacity:0.0;
    box-shadow:0 0 14px rgba(255,255,255,0.8);
    pointer-events:none;
    z-index:6;
    animation:blink 1.4s linear infinite;
  }
  @keyframes blink {
    0% { opacity:0; transform:scale(.6); }
    50%{ opacity:1; transform:scale(1.2); }
    100%{ opacity:0; transform:scale(.6); }
  }

  /* small footer note */
  .hint{font-size:12px;color:#cbbcd0;margin-top:14px;text-align:center;}
  footer{font-size:11px;color:#8f7f95;margin-top:8px;text-align:center;}
  @media (max-width:420px){
    h1{font-size:18px}
    button.choice{padding:10px;font-size:14px;}
  }
</style>
</head>
<body>
  <div class="card" role="dialog" aria-labelledby="title">
    <div class="glow"></div>
    <h1 id="title">tối nay khó ngủ quá — có muốn biết lý do không?</h1>
    <p class="lead">Chọn một trong hai nhé — mình cài tí nhạc và hiệu ứng để lãng mạn hơn.</p>

    <div class="choices" role="group" aria-label="Lựa chọn">
      <button id="yes" class="choice">Có</button>
      <button id="no"  class="choice">Không</button>
    </div>

    <div id="result" class="result" aria-live="polite"></div>
    <div class="hint">Tip: bấm phím Y = Có, N = Không</div>
    <footer>— GibThu của bạn 💌</footer>

    <div class="hearts" id="hearts"></div>
  </div>

<script>
/* ----- UI logic ----- */
const yes = document.getElementById('yes');
const no  = document.getElementById('no');
const result = document.getElementById('result');
const heartsContainer = document.getElementById('hearts');

function showResult(text, opts={play:false}) {
  result.textContent = text;
  result.classList.add('show');
  if(opts.play) startRomantic();
  else stopRomantic();
}

/* keep references for audio nodes */
let audioCtx = null;
let masterGain = null;
let playing = false;
let droneNodes = [];

/* Create a soft arpeggiated romantic loop using WebAudio */
function startRomantic(){
  if(playing) return;
  try {
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    masterGain = audioCtx.createGain();
    masterGain.gain.value = 0.16;
    masterGain.connect(audioCtx.destination);

    // gentle chord notes (A minor-ish warm)
    const chord = [220.00, 277.18, 330.00]; // A3, C#4, E4-ish for color
    // schedule repeating soft plucks
    const now = audioCtx.currentTime;
    for(let i=0;i<3;i++){
      const t = now + i*0.12;
      const osc = audioCtx.createOscillator();
      const gain = audioCtx.createGain();
      osc.type = 'sine';
      osc.frequency.value = chord[i];
      gain.gain.value = 0.0;
      // envelope
      gain.gain.setValueAtTime(0.0, t);
      gain.gain.linearRampToValueAtTime(0.18, t+0.04);
      gain.gain.exponentialRampToValueAtTime(0.001, t+2.6);
      // filter for warmth
      const filter = audioCtx.createBiquadFilter();
      filter.type = 'lowpass';
      filter.frequency.value = 1200;
      osc.connect(filter);
      filter.connect(gain);
      gain.connect(masterGain);

      osc.start(t);
      osc.stop(t+3.2);

      // keep a reference to stop later
      droneNodes.push({osc, gain});
    }

    // subtle tremolo/pulsing
    const lfo = audioCtx.createOscillator();
    lfo.type = 'sine';
    lfo.frequency.value = 0.35;
    const lfoGain = audioCtx.createGain(); lfoGain.gain.value = 0.1;
    lfo.connect(lfoGain);
    lfoGain.connect(masterGain.gain);
    lfo.start();

    playing = true;

    // keep looping by scheduling more notes every 2.2s
    scheduleLoop();
  } catch(e){
    console.warn("audio start error", e);
  }
}
function scheduleLoop(){
  if(!playing) return;
  // schedule repeating soft chord every ~2.2s
  loopTimeout = setTimeout(()=>{
    if(!playing) return;
    // create a short cluster of pluck notes
    const chord = [220.00, 277.18, 330.00];
    const now = audioCtx.currentTime;
    for(let i=0;i<3;i++){
      const t = now + i*0.09;
      const osc = audioCtx.createOscillator();
      const gain = audioCtx.createGain();
      osc.type = 'sine';
      osc.frequency.value = chord[i] * (1 + (Math.random()-0.5)*0.02);
      gain.gain.value = 0.0;
      gain.gain.setValueAtTime(0.0, t);
      gain.gain.linearRampToValueAtTime(0.18, t+0.03);
      gain.gain.exponentialRampToValueAtTime(0.001, t+2.2);
      const filter = audioCtx.createBiquadFilter();
      filter.type = 'lowpass';
      filter.frequency.value = 1300 + Math.random()*200;
      osc.connect(filter);
      filter.connect(gain);
      gain.connect(masterGain);
      osc.start(t);
      osc.stop(t+2.6);
      droneNodes.push({osc,gain});
    }
    scheduleLoop();
  }, 2200 + Math.random()*400);
}
function stopRomantic(){
  if(!playing) return;
  try {
    // graceful stop
    droneNodes.forEach(n=>{
      try{ n.osc.stop(); }catch(e){}
      try{ n.gain.disconnect(); }catch(e){}
    });
    droneNodes = [];
    if(masterGain) masterGain.gain.setTargetAtTime(0, audioCtx.currentTime, 0.2);
    if(audioCtx) {
      setTimeout(()=> {
        try{ audioCtx.close(); }catch(e){}
        audioCtx = null;
      }, 400);
    }
  } catch(e){}
  playing = false;
}

/* heart emitter */
let heartInterval = null;
function startHearts(){
  if(heartInterval) return;
  heartInterval = setInterval(()=> {
    createHeart();
  }, 220);
}
function stopHearts(){
  if(!heartInterval) return;
  clearInterval(heartInterval);
  heartInterval = null;
  // remove remaining hearts gradually
  setTimeout(()=> {
    heartsContainer.innerHTML = '';
  }, 1200);
}
function createHeart(){
  const h = document.createElement('div');
  h.className = 'heart';
  const left = (20 + Math.random()*60) + '%';
  const size = 14 + Math.random()*26;
  h.style.left = left;
  h.style.bottom = (10 + Math.random()*10) + 'px';
  h.style.width = size + 'px';
  h.style.height = size + 'px';
  const dur = 3800 + Math.random()*1600;
  h.style.animationDuration = dur + 'ms';
  heartsContainer.appendChild(h);
  // remove after animation
  setTimeout(()=> {
    h.remove();
  }, dur + 80);
}

/* small sparkle generator */
function startSparkles(){
  for(let i=0;i<8;i++){
    const s = document.createElement('div');
    s.className = 'sparkle';
    s.style.left = (10 + Math.random()*80) + '%';
    s.style.top  = (8 + Math.random()*70) + '%';
    s.style.animationDelay = (Math.random()*1.6) + 's';
    s.style.opacity = 0.0;
    document.body.appendChild(s);
    setTimeout(()=> s.remove(), 5200);
  }
}

/* handle choices */
yes.addEventListener('click', ()=> {
  showResult('vì anh nhớ emm đó', {play:true});
  startHearts();
  startSparkles();
});
no.addEventListener('click', ()=> {
  showResult('k chạm được', {play:false});
  stopHearts();
});

/* keyboard shortcuts */
document.addEventListener('keydown', (e)=>{
  if(e.key.toLowerCase() === 'y') yes.click();
  if(e.key.toLowerCase() === 'n') no.click();
});

/* accessibility: focus styles */
[yes,no].forEach(btn=>{
  btn.addEventListener('focus', ()=> btn.style.outline = '3px solid rgba(255,107,159,0.18)');
  btn.addEventListener('blur', ()=> btn.style.outline = 'none');
});

/* pause audio when tab hidden */
document.addEventListener('visibilitychange', ()=>{
  if(document.hidden) stopRomantic();
});

</script>
</body>
</html>
