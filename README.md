<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Lulu's Puppies ♡</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#241039;color:white;font-family:system-ui;text-align:center}
h1{color:#ff9ed9;text-shadow:0 0 18px #ff48b4}
main{max-width:1000px;margin:auto;padding:16px}
.stage{position:relative;min-height:420px;overflow:hidden;border:3px solid #ff9ed9;border-radius:22px;background:linear-gradient(#27194f,#a254a1,#ff9fca)}
.moon{position:absolute;right:9%;top:8%;width:65px;height:65px;border-radius:50%;background:#fff2c5;box-shadow:0 0 35px white}
.speech{position:relative;z-index:5;margin:65px auto 0;width:fit-content;max-width:90%;padding:12px 18px;border-radius:20px;background:white;color:#62265f;font-weight:bold}
.cast{position:absolute;bottom:25px;left:1%;right:1%;display:flex;justify-content:center;align-items:end;gap:1.2%;z-index:2}
.girl{--hair:#422323;--dress:#ff80c6;--skin:#dca184;position:relative;width:10%;min-width:30px;animation:dance .7s infinite alternate ease-in-out}
.girl.tall{width:11%}
.girl.lulu{width:12%;--hair:#80502f;--dress:#ff3eaa;--skin:#f2d5c2}
.crown{height:27px;color:#ffe17b;font-size:24px}
.head{position:relative;width:70%;aspect-ratio:1;margin:auto;background:var(--skin);border:2px solid #43203c;border-radius:48%}
.hair{position:absolute;top:-7%;left:-5%;width:110%;height:52%;background:var(--hair);border-radius:60% 60% 25% 25%}
.long .hair:after{content:"";position:absolute;top:55%;left:0;width:100%;height:100%;background:var(--hair);border-radius:0 0 12px 12px}
.eyes{position:absolute;left:22%;top:52%;width:8%;height:12%;border-radius:50%;background:#392039;box-shadow:16px 0 #392039}
.lulu .eyes{background:#258f53;box-shadow:16px 0 #258f53}
.glasses{position:absolute;top:43%;left:9%;width:82%;height:27%;border:2px solid #29202f;border-radius:8px}
.smile{position:absolute;top:69%;left:40%;width:23%;height:8%;border-bottom:2px solid #a53c6a;border-radius:50%}
.body{width:80%;height:58px;margin:auto;background:var(--dress);border:2px solid #43203c;border-radius:30% 30% 8% 8%}
.legs{display:flex;justify-content:center;gap:14%;height:24px}
.legs i{width:8px;background:var(--skin);border:2px solid #43203c;border-radius:0 0 6px 6px}
.label{height:14px;font-size:9px}
@keyframes dance{from{transform:translateY(0) rotate(-4deg)}to{transform:translateY(-16px) rotate(4deg)}}
.hearts{position:absolute;inset:0;pointer-events:none}
.heart{position:absolute;bottom:15%;animation:float 3s infinite;left:var(--x);font-size:25px}
@keyframes float{to{transform:translateY(-300px) rotate(25deg);opacity:0}}
.caption{padding:18px;font-size:1.15rem;font-weight:bold;min-height:85px}
button{margin:4px;padding:10px 15px;border:0;border-radius:30px;background:#ff9ed9;color:#35113b;font-weight:bold;cursor:pointer}
audio{width:min(95%,450px);margin:12px}
@media(max-width:500px){.stage{min-height:340px}.body{height:42px}.girl{min-width:23px}.legs{height:17px}.speech{font-size:13px}}
</style>
</head>
<body>
<main>
<h1>🐾 LULU'S PUPPIES ♡</h1>
<p>Seven girls. One queen. Maximum woof.</p>
<section class="stage">
<div class="moon"></div>
<div class="speech" id="speech">Lulu's here! Oh, look at all my girls!</div>
<div class="hearts" id="hearts"></div>
<div class="cast" id="cast"></div>
</section>
<div class="caption" id="caption">Come on, then. Let Mommy hear you. Woof, woof!</div>
<div>
<button onclick="play()">▶ Play / Pause</button>
<button onclick="prev()">← Previous</button>
<button onclick="next()">Next scene →</button>
<button onclick="restart()">↺ Restart</button>
</div>
<p>Add your song here:</p>
<input id="file" type="file" accept="audio/*">
<br><audio id="audio" controls></audio>
</main>
<script>
const people=[
 {h:"#d64a50",d:"#ff7ab7",s:"#c98b6b",short:1},
 {h:"#4b2b28",d:"#a68aff",s:"#e2ad8d",long:1},
 {h:"#754a36",d:"#71d7ff",s:"#d99b7c",short:1,glasses:1,tall:1},
 {h:"#3b211e",d:"#ffbe69",s:"#a96d50",long:1,tall:1},
 {h:"#4c2d25",d:"#9be5c4",s:"#c78b6a",long:1},
 {h:"#62402d",d:"#ff83bd",s:"#f4d7c8",bun:1},
 {h:"#5a3028",d:"#b5a0ff",s:"#edbd9d",long:1,tall:1},
 {h:"#80502f",d:"#ff3eaa",s:"#f2d5c2",long:1,lulu:1}
];
const scenes=[
 ["INTRO","Lulu's here! Oh, look at all my girls!","Come on, then. Let Mommy hear you. Woof, woof!"],
 ["VERSE 1","Seven pretty girls with their eyes on the queen!","You're interesting, babe."],
 ["PRE-CHORUS","She says, Come here, and they come running fast!","Who's my girl?"],
 ["CHORUS","We're Lulu's puppies! Woof, woof, woof!","THAT'S A GOOD GIRL!"],
 ["POST-CHORUS","Who's that girl? LULU! Who's she love? HER GIRLS!","Who's Mommy's favourite? ME! ME! ME!"],
 ["VERSE 2","Seven little crushes in seven different places!","Yummy! Oh, my goodness!"],
 ["CHEEKY MOMENT","What? I was talking about picking up your things!","Such bad girls!"],
 ["INTERLUDE","Why are you all so crazy? BECAUSE WE LOVE YOU!","COLLECTIVE SCREAMING!"],
 ["BRIDGE","Behind every bark, there's a heart beating fast.","Mommy's proud of every one of you."],
 ["FINAL CHORUS","Crazy, cutesy, loyal and true!","NOBODY DOES CRAZY LIKE OUR FAMILY!"],
 ["OUTRO","You're all my favourites, you crazy girls!","MOMMY'S PROUD! WOOF!"]
];
let i=0,timer=null,playing=false;
const cast=document.querySelector("#cast");
people.forEach(p=>{
 const el=document.createElement("div");
 el.className="girl "+(p.tall?"tall ":"")+(p.lulu?"lulu ":"")+(p.long?"long ":"");
 el.style.setProperty("--hair",p.h);
 el.style.setProperty("--dress",p.d);
 el.style.setProperty("--skin",p.s);
 el.innerHTML=`<div class="crown">${p.lulu?"♛":"♡"}</div><div class="head"><div class="hair"></div><div class="eyes"></div>${p.glasses?'<div class="glasses"></div>':""}<div class="smile"></div></div><div class="body"></div><div class="legs"><i></i><i></i></div><div class="label"></div>`;
 cast.appendChild(el);
});
function render(){
 const s=scenes[i];
 document.querySelector("#speech").textContent=s[1];
 document.querySelector("#caption").textContent=s[2];
 document.querySelector("#hearts").innerHTML=Array.from({length:12},(_,n)=>`<span class="heart" style="--x:${n*8}%;animation-delay:${Math.random()*2}s">${["♥","♡","✦","🐾"][n%4]}</span>`).join("");
}
function next(){i=(i+1)%scenes.length;render()}
function prev(){i=(i-1+scenes.length)%scenes.length;render()}
function restart(){clearInterval(timer);playing=false;i=0;render()}
function play(){
 if(playing){clearInterval(timer);playing=false;return}
 playing=true;render();
 timer=setInterval(()=>{if(i===scenes.length-1){clearInterval(timer);playing=false;return}next()},4000);
}
document.querySelector("#file").addEventListener("change",e=>{
 const f=e.target.files[0];if(f){const a=document.querySelector("#audio");a.src=URL.createObjectURL(f);a.play().catch(()=>{});if(!playing)play()}
});
render();
</script>
</body>
</html>
