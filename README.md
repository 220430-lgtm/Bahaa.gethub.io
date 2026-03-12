<!DOCTYPE html>
<html>

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>

body{
margin:0;
background:black;
overflow:hidden;
font-family:Arial;
}

canvas{
position:fixed;
top:0;
left:0;
}

#glassBox{

position:fixed;
top:50%;
left:50%;
transform:translate(-50%,-50%);
width:70%;
max-width:700px;
height:320px;

padding:30px;

color:white;
font-size:18px;
line-height:1.9;

text-align:center;

border-radius:25px;

background:rgba(255,255,255,0.08);
backdrop-filter:blur(12px);
-webkit-backdrop-filter:blur(12px);

border:1px solid rgba(255,255,255,0.2);

box-shadow:0 0 40px rgba(255,0,80,0.2);

display:none;

overflow-y:auto;
scroll-behavior:smooth;

}

</style>

</head>

<body>

<canvas id="canvas"></canvas>

<div id="glassBox">
<p id="loveText"></p>
</div>

<script>

const canvas=document.getElementById("canvas")
const ctx=canvas.getContext("2d")

canvas.width=window.innerWidth
canvas.height=window.innerHeight

let W=canvas.width
let H=canvas.height



let columns=Math.floor(W/6)
let drops=[]

for(let i=0;i<columns;i++){
drops[i]=Math.random()*H
}

let matrixAlpha=1



let particles=[]



function buildText(text){

let off=document.createElement("canvas")
let t=off.getContext("2d")

off.width=800
off.height=300

t.fillStyle="white"
t.textAlign="center"



if(text==="3" || text==="2" || text==="1"){
t.font="bold 120px Arial"
}

else if(text==="❤"){
t.font="bold 130px Arial"
}

else if(text==="كل عام وانتي بخير يا حبيبتي"){
t.font="bold 30px Arial"
}

else if(/[\u0600-\u06FF]/.test(text)){
t.font="bold 40px Arial"
}

else{
t.font="bold 80px Arial"
}

t.fillText(text,400,180)

let data=t.getImageData(0,0,800,300)

particles=[]

for(let y=0;y<300;y+=2){
for(let x=0;x<800;x+=2){

let i=(y*800+x)*4

if(data.data[i+3]>128){

particles.push({

x:Math.random()*W,
y:Math.random()*H,

tx:x+W/2-400,
ty:y+H/2-150

})

}

}
}

}



let explosion=[]



function explode(){

particles.forEach(p=>{

explosion.push({

x:p.x,
y:p.y,
vx:(Math.random()-0.5)*14,
vy:(Math.random()-0.5)*14,
life:100

})

})

particles=[]

}



let stars=[]



function createStars(){

for(let i=0;i<200;i++){

stars.push({

x:Math.random()*W,
y:Math.random()*H,
size:Math.random()*2,
phase:Math.random()*10

})

}

}



function draw(){

ctx.fillStyle="rgba(0,0,0,0.08)"
ctx.fillRect(0,0,W,H)



ctx.fillStyle="rgba(255,0,60,"+matrixAlpha+")"
ctx.font="8px monospace"

for(let i=0;i<columns;i++){

ctx.fillText("❤",i*6,drops[i])

drops[i]+=3

if(drops[i]>H){
drops[i]=0
}

}



ctx.fillStyle="#d81b60"
ctx.font="3px monospace"

particles.forEach(p=>{

p.x+=(p.tx-p.x)*0.08
p.y+=(p.ty-p.y)*0.08

ctx.fillText("❤",p.x,p.y)

})



ctx.fillStyle="#d81b60"

explosion.forEach(e=>{

ctx.fillText("❤",e.x,e.y)

e.x+=e.vx
e.y+=e.vy

e.life--

})

explosion=explosion.filter(e=>e.life>0)



stars.forEach(s=>{

let glow=Math.sin(Date.now()*0.002+s.phase)

ctx.fillStyle="rgba(255,255,255,"+(0.3+glow)+")"

ctx.beginPath()
ctx.arc(s.x,s.y,s.size,0,Math.PI*2)
ctx.fill()

})



requestAnimationFrame(draw)

}



draw()



setTimeout(()=>buildText("3"),4000)
setTimeout(()=>buildText("2"),6000)
setTimeout(()=>buildText("1"),8000)

setTimeout(()=>buildText("HAPPY"),10000)
setTimeout(()=>buildText("BIRTHDAY"),12000)
setTimeout(()=>buildText("TO YOU"),14000)
setTimeout(()=>buildText("AYA"),16000)

setTimeout(()=>buildText("❤"),18000)



setTimeout(()=>{

explode()

},20000)



setTimeout(()=>{

let fade=setInterval(()=>{

matrixAlpha-=0.015

if(matrixAlpha<=0){

clearInterval(fade)

explosion=[]

createStars()

setTimeout(()=>{

buildText("كل عام وانتي بخير يا حبيبتي")

setTimeout(()=>{

particles=[]

document.getElementById("glassBox").style.display="block"

startTyping()

},4000)

},2000)

}

},40)

},20000)



const message=`حبيت اعايد عليكي يا حبيبتي قبل الكل وحبيت اني ابدا في كلامي الك ومشاعري اتجاهك وحبي الكبير
كل عام وانتي بخير كل عام واحنا مع بعض بكل الأعياد
كل عام وانتي عيدي وفرحه ايامي انتي الي بتحلي أيامي وبتسعد حياتي وتسعد قلبي
انتي الفرحه الي ما أمل منها انتي العمر الي اتمناه ل قلبي انتي الحب الاول والاخير في قلبي
انتي عيدي وكل أعيادي انتي كل الكون والله وعيدي وخيري وحبي وروحي وعمري وكل اشي فيني
انتي الفرحه حياتي انتي حبيبة روحي وحبيبة القلب والعمر والعشق
انت دربي يا روحي وكل دروبي انتي عيدي قبل العيد
انتي العمر قبل الروح انتي القلب قبل الحياه
انتي العشق قبل الحب انتي المشاعر قبل الشعور
انتي الهدف في الحياه انتي الشخص الي بتمناه
انتي النصيب الي بتمنى وبدعي يقسمه لي رب العالمين
انتي العيد الي اتمناه كل يوم عيد لي
انتي الفرحه وسعاده انتي الحب والعشق
انتي زينة الحياه وحب الروح وعشق القلب
انت الوريد الي يعيش بوجودو قلبي

بحبك بحبك بحبك

يا عيدي ويانصيبي بحبك يافرحتي وسعادتي
بحبك بحبك بحبك

وكل عام وانتي نصيبي
وكل عام وانتي فرحتي
وكل عام وقلبي فيكي يتبارك

كل عام وانتي بخير يا وريد القلب ويا عشق القلب
بحبك 🥹🫂`

let i=0

function startTyping(){

if(i<message.length){

document.getElementById("loveText").innerHTML+=message.charAt(i)

i++

setTimeout(startTyping,70)

}

}



setInterval(()=>{

const box=document.getElementById("glassBox")

if(box.scrollTop < box.scrollHeight - box.clientHeight){

box.scrollTop += 0.4

}

},30)



</script>

</body>

</html>
