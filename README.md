<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#0757b8">
<title>Labib Telecom | Spin & Win</title>
<style>
:root{--blue:#0757b8;--navy:#062b63;--green:#078b45;--gold:#ffd34e}
*{box-sizing:border-box}
body{margin:0;font-family:system-ui,"Noto Sans Bengali",sans-serif;background:linear-gradient(160deg,#eaf6ff,#fff7df);color:#10284a}
.wrap{max-width:760px;margin:auto;padding:18px}
header{text-align:center;background:linear-gradient(135deg,#064aa2,#087bd0);color:white;padding:22px 16px;border-radius:22px;box-shadow:0 8px 22px #063c7b33}
.brand-mark{width:82px;height:82px;border:4px solid white;border-radius:50%;margin:0 auto 9px;background:#fff;color:#0757b8;display:grid;place-items:center;font-weight:900;font-size:14px;line-height:1.1;box-shadow:0 3px 12px #001c48aa}
h1{font-size:clamp(25px,6vw,38px);margin:5px 0;color:#fff}
.tag{margin:5px 0 0;color:#e8f6ff}
.sub{font-size:14px;color:#526982;text-align:center;margin:16px 0}
.panel{background:#fff;border-radius:22px;padding:18px;margin-top:16px;box-shadow:0 8px 24px #183e6818}
.wheel-area{position:relative;width:min(88vw,390px);aspect-ratio:1;margin:10px auto 18px}
canvas{width:100%;height:100%;display:block;filter:drop-shadow(0 8px 8px #12365a30)}
.pointer{position:absolute;z-index:2;left:50%;top:-5px;transform:translateX(-50%);width:0;height:0;border-left:19px solid transparent;border-right:19px solid transparent;border-top:38px solid #e62929;filter:drop-shadow(0 3px 2px #555)}
.spin{display:block;width:min(100%,330px);margin:10px auto;background:linear-gradient(#ffdf58,#ffad00);border:0;border-radius:50px;padding:15px 20px;font-size:21px;font-weight:900;color:#5a2600;box-shadow:0 5px 0 #c77a00;cursor:pointer}
.spin:disabled{opacity:.55;cursor:not-allowed}
#result{text-align:center;min-height:35px;font-size:20px;font-weight:800;color:#087b42;margin:12px 0}
.note{font-size:12px;color:#718198;text-align:center;line-height:1.6}
h2{color:#0757b8;text-align:center;margin:4px 0 14px}
.services{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:10px}
.service{background:#f1f7ff;border:1px solid #d8e9fc;border-radius:13px;padding:12px;font-weight:650;font-size:14px}
footer{text-align:center;color:#5b7188;font-size:13px;padding:20px 5px}
@media(min-width:560px){.services{grid-template-columns:repeat(3,minmax(0,1fr))}}
</style>
</head>
<body>
<div class="wrap">
<header>
  <div class="brand-mark">LABIB<br>TELECOM</div>
  <h1>🎁 SPIN &amp; WIN 🎡</h1>
  <p class="tag">স্পিন করুন, জিতে নিন আকর্ষণীয় অফার!</p>
  <p class="tag"><small>স্বাধীনতার মাসে আনন্দের উপহার</small></p>
</header>

<p class="sub">Labib Telecom-এর পক্ষ থেকে আপনার জন্য বিশেষ আয়োজন</p>

<section class="panel">
  <div class="wheel-area">
    <div class="pointer"></div>
    <canvas id="wheel" width="700" height="700" aria-label="পুরস্কারের চাকা"></canvas>
  </div>
  <button class="spin" id="spinBtn">চাকা ঘোরান</button>
  <div id="result" aria-live="polite">আপনার ভাগ্য পরীক্ষা করুন!</div>
  <p class="note">এই সংস্করণটি প্রাথমিক ডেমো। একই ব্রাউজারে একবার স্পিনের সীমা রাখা হয়েছে।<br>
  প্রকৃত ক্যাম্পেইনে এক ব্যক্তি একবার, পুরস্কারের সংখ্যা ও বিজয়ীর রেকর্ড নিশ্চিত করতে সার্ভার/ডেটাবেস সংযোগ লাগবে।</p>
</section>

<section class="panel">
  <h2>আমাদের সেবাসমূহ</h2>
  <div class="services">
    <div class="service">📱 সব অপারেটরের মোবাইল রিচার্জ</div>
    <div class="service">🌐 ইন্টারনেট ও মিনিট প্যাক</div>
    <div class="service">💳 বিকাশ, নগদ, রকেট ও উপায়</div>
    <div class="service">⚡ বিদ্যুৎ বিল পরিশোধ</div>
    <div class="service">💧 পানির বিল পরিশোধ</div>
    <div class="service">🏦 ক্যাশ ইন ও ক্যাশ আউট</div>
    <div class="service">💸 সেন্ড মানি ও মোবাইল ব্যাংকিং</div>
    <div class="service">🎯 ড্রাইভ অফার ও প্যাক</div>
    <div class="service">➕ অ্যাড ব্যালেন্স</div>
  </div>
</section>
<footer>Labib Telecom — দ্রুত সেবা, নির্ভরযোগ্য লেনদেন</footer>
</div>
<script>
const prizes = ["৳৫","৳১০","৳২০","৳৩০","৳৫০","৳৯৯","৳০"];
const colors = ["#087bdb","#ff9d00","#8b36d9","#078b45","#e62e82","#0757b8","#777f8c"];
const canvas = document.getElementById("wheel"), ctx = canvas.getContext("2d");
const cx=350, cy=350, radius=325, slice=Math.PI*2/prizes.length;
let rotation=0, spinning=false;
function draw(){
  ctx.clearRect(0,0,700,700);
  prizes.forEach((p,i)=>{
    const start=rotation+i*slice-Math.PI/2, end=start+slice;
    ctx.beginPath();ctx.moveTo(cx,cy);ctx.arc(cx,cy,radius,start,end);ctx.closePath();
    ctx.fillStyle=colors[i];ctx.fill();ctx.lineWidth=7;ctx.strokeStyle="#fff";ctx.stroke();
    ctx.save();ctx.translate(cx,cy);ctx.rotate(start+slice/2);
    ctx.textAlign="right";ctx.fillStyle="#fff";ctx.font="bold 43px system-ui, sans-serif";
    ctx.shadowColor="#0008";ctx.shadowBlur=4;ctx.fillText(p, radius-28, 15);ctx.restore();
  });
  ctx.beginPath();ctx.arc(cx,cy,76,0,Math.PI*2);ctx.fillStyle="#fff";ctx.fill();ctx.lineWidth=10;ctx.strokeStyle="#ffd34e";ctx.stroke();
  ctx.fillStyle="#0757b8";ctx.textAlign="center";ctx.font="bold 25px system-ui";ctx.fillText("LABIB",cx,cy-5);ctx.fillText("WIN",cx,cy+27);
}
draw();
const btn=document.getElementById("spinBtn"), result=document.getElementById("result");
if(localStorage.getItem("labib_spin_demo_used")==="yes"){
  btn.disabled=true;result.textContent="এই ব্রাউজারে স্পিনের সুযোগ ব্যবহার করা হয়েছে।";
}
btn.addEventListener("click",()=>{
  if(spinning || localStorage.getItem("labib_spin_demo_used")==="yes") return;
  spinning=true;btn.disabled=true;result.textContent="চাকা ঘুরছে...";
  const winner=Math.floor(Math.random()*prizes.length);
  const target=(Math.PI*2*6)+(Math.PI*2-(winner*slice+slice/2));
  const start=rotation, duration=4300, began=performance.now();
  function animate(now){
    const t=Math.min(1,(now-began)/duration), ease=1-Math.pow(1-t,4);
    rotation=start+target*ease;draw();
    if(t<1) requestAnimationFrame(animate);
    else{
      spinning=false;localStorage.setItem("labib_spin_demo_used","yes");
      result.textContent=winner===6?"এবার কোনো পুরস্কার জেতা হয়নি। আবারও Labib Telecom-এর সঙ্গে থাকুন!":"অভিনন্দন! আপনি জিতেছেন "+prizes[winner]+" বোনাস!";
      btn.textContent="স্পিন সম্পন্ন"; 
    }
  }
  requestAnimationFrame(animate);
});
</script>
</body>
</html>