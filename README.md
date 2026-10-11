<!DOCTYPE html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>English Secret ✨</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f8f1eb;color:#574638}
header{background:#fffaf6;padding:25px 15px;text-align:center;border-bottom:1px solid #ead9cb}
header h1{color:#a47b60;margin:0 0 8px}
header p{margin:0;color:#806b5b}
main{max-width:720px;margin:25px auto;padding:0 15px}
.panel{background:white;border-radius:18px;padding:22px;margin-bottom:16px;box-shadow:0 3px 12px #e8dacf}
h2{color:#956d52}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px}
.category{background:#fff;border:1px solid #ead9cb;border-radius:16px;padding:22px;text-align:left;cursor:pointer;color:#574638}
.category strong{display:block;font-size:18px;margin-bottom:9px;color:#956d52}
.category span{font-size:14px;line-height:1.5}
button{font-size:16px}
.primary,.answer,.back{border:0;border-radius:10px;padding:13px 16px;cursor:pointer}
.primary,.back{background:#ad8568;color:white}
.answer{display:block;width:100%;margin:10px 0;background:#f7eee7;color:#574638;border:1px solid #e5d2c2;text-align:left}
.answer:disabled{cursor:default;opacity:1}
.answer.correct{background:#dcebdc;border-color:#7da47d}
.answer.wrong{background:#f5dddd;border-color:#cc8888}
.hidden{display:none!important}
#feedback{font-weight:bold;line-height:1.5}
.small{font-size:14px;color:#806b5b}
footer{text-align:center;padding:25px;color:#806b5b}
</style>
</head>
<body>
<header>
<h1>English Secret ✨</h1>
<p>Step by Step — Learn English!</p>
</header>

<main>
<section id="home" class="panel">
<h2>Welcome to English Secret! 🌷</h2>
<p>Choose a section and practise your English.</p>
<div class="grid">
<button class="category" onclick="openSection('grammar')">
<strong>📚 Grammar Tests</strong>
<span>Present Simple, tenses and grammar rules</span>
</button>
<button class="category" onclick="openSection('vocabulary')">
<strong>📝 Vocabulary Tests</strong>
<span>Word meanings and vocabulary practice</span>
</button>
<button class="category" onclick="openSection('reading')">
<strong>📖 Reading Tests</strong>
<span>Read a text and answer questions</span>
</button>
<button class="category" onclick="showResults()">
<strong>🏆 My Results</strong>
<span>See your completed tests and scores</span>
</button>
</div>
</section>

<section id="section" class="panel hidden">
<button class="back" onclick="goHome()">← Ana səhifə</button>
<h2 id="sectionTitle"></h2>
<div id="testList"></div>
</section>

<section id="quiz" class="panel hidden">
<button class="back" onclick="goSections()">← Testlərə qayıt</button>
<h2 id="quizTitle"></h2>
<p id="progress" class="small"></p>
<h3 id="question"></h3>
<div id="answers"></div>
<p id="feedback" aria-live="polite"></p>
<button id="next" class="primary hidden" onclick="nextQuestion()">Növbəti sual →</button>
<div id="finish" class="hidden">
<h3 id="finalScore"></h3>
<button class="primary" onclick="goSections()">Digər testlər</button>
</div>
</section>

<section id="results" class="panel hidden">
<button class="back" onclick="goHome()">← Ana səhifə</button>
<h2>🏆 My Results</h2>
<div id="resultList"></div>
</section>
</main>

<footer>English Secret ✨ | Learn something new every day!</footer>

<script>
const tests = {
grammar: {
title:"📚 Grammar Tests",
items:[
{title:"Present Simple",questions:[
{q:"She ___ to school every day.",a:["go","goes","going"],c:1},
{q:"They ___ football on Sundays.",a:["plays","play","playing"],c:1},
{q:"He ___ like coffee.",a:["don't","doesn't","isn't"],c:1},
{q:"I ___ English every day.",a:["study","studies","studying"],c:0},
{q:"___ she work here?",a:["Do","Does","Is"],c:1}
]},
{title:"Present Continuous",questions:[
{q:"I ___ a book now.",a:["read","am reading","reads"],c:1},
{q:"They ___ playing outside.",a:["is","am","are"],c:2},
{q:"She ___ TV at the moment.",a:["is watching","watches","watch"],c:0}
]},
{title:"Past Simple",questions:[
{q:"We ___ to the park yesterday.",a:["go","went","going"],c:1},
{q:"She ___ her homework last night.",a:["finished","finish","finishes"],c:0},
{q:"Did you ___ the film?",a:["saw","seeing","see"],c:2}
]}
]},
vocabulary:{
title:"📝 Vocabulary Tests",
items:[
{title:"Everyday Vocabulary",questions:[
{q:"What is the opposite of 'big'?",a:["Tall","Small","Long"],c:1},
{q:"What does 'begin' mean?",a:["Start","Finish","Forget"],c:0},
{q:"Choose the correct word: I am ___ because I need sleep.",a:["hungry","tired","thirsty"],c:1}
]},
{title:"Synonyms",questions:[
{q:"Choose a synonym of 'happy'.",a:["Glad","Angry","Sad"],c:0},
{q:"Choose a synonym of 'quick'.",a:["Slow","Fast","Late"],c:1},
{q:"Choose a synonym of 'clever'.",a:["Intelligent","Lazy","Weak"],c:0}
]}
]},
reading:{
title:"📖 Reading Tests",
items:[
{title:"A Day in Anna's Life",passage:"Anna is a student. She gets up at seven o'clock every morning. She has breakfast and goes to school by bus. Her favourite subject is English. After school, she reads books and helps her mother.",questions:[
{q:"What time does Anna get up?",a:["At six","At seven","At eight"],c:1},
{q:"How does she go to school?",a:["By bus","By car","On foot"],c:0},
{q:"What is her favourite subject?",a:["Maths","Science","English"],c:2},
{q:"What does she do after school?",a:["Plays tennis","Reads books","Goes shopping"],c:1}
]},
{title:"Tom's Weekend",passage:"Tom lives in a small town. On Saturdays, he plays football with his friends. On Sundays, he visits his grandmother and helps her in the garden. He enjoys spending time with his family.",questions:[
{q:"Where does Tom live?",a:["In a small town","In a big city","In a village abroad"],c:0},
{q:"What does he play on Saturdays?",a:["Basketball","Football","Tennis"],c:1},
{q:"Who does he visit on Sundays?",a:["His teacher","His cousin","His grandmother"],c:2}
]}
]}
};

let sectionKey="",testIndex=0,questionIndex=0,score=0,locked=false;
let sessionScores=[];
let history=[];

function hideAll(){
["home","section","quiz","results"].forEach(id=>
document.getElementById(id).classList.add("hidden"));
}
function goHome(){hideAll();document.getElementById("home").classList.remove("hidden")}
function goSections(){openSection(sectionKey)}
function openSection(key){
sectionKey=key;hideAll();
document.getElementById("section").classList.remove("hidden");
document.getElementById("sectionTitle").textContent=tests[key].title;
const list=document.getElementById("testList");
list.innerHTML="";
tests[key].items.forEach((item,i)=>{
const b=document.createElement("button");
b.className="category";
b.style.width="100%";
b.style.marginTop="12px";
const title=document.createElement("strong");
title.textContent=(i+1)+". "+item.title;
const detail=document.createElement("span");
detail.textContent=item.questions.length+" questions";
b.append(title,detail);
b.onclick=()=>startTest(i);
list.appendChild(b);
});
}
function startTest(index){
testIndex=index;questionIndex=0;score=0;locked=false;
sessionScores=[];
hideAll();
document.getElementById("quiz").classList.remove("hidden");
document.getElementById("finish").classList.add("hidden");
document.getElementById("quizTitle").textContent=tests[sectionKey].items[index].title;
showQuestion();
}
function showQuestion(){
locked=false;
const item=tests[sectionKey].items[testIndex];
const q=item.questions[questionIndex];
document.getElementById("progress").textContent=
"Question "+(questionIndex+1)+" / "+item.questions.length;
document.getElementById("question").textContent=q.q;
document.getElementById("feedback").textContent="";
document.getElementById("next").classList.add("hidden");
const box=document.getElementById("answers");
box.innerHTML="";
if(item.passage && questionIndex===0){
const passage=document.createElement("p");
passage.textContent=item.passage;
passage.style.lineHeight="1.7";
box.appendChild(passage);
}
q.a.forEach((answer,i)=>{
const b=document.createElement("button");
b.className="answer";
b.textContent=String.fromCharCode(65+i)+". "+answer;
b.onclick=()=>checkAnswer(i);
box.appendChild(b);
});
}
function checkAnswer(choice){
if(locked)return;
locked=true;
const item=tests[sectionKey].items[testIndex];
const q=item.questions[questionIndex];
const correct=choice===q.c;
if(correct)score++;
sessionScores.push(correct);
document.getElementById("feedback").textContent=correct?
"Correct! 🌟 Düzgün cavab!":"Düzgün cavab: "+q.a[q.c];
document.querySelectorAll("#answers .answer").forEach((b,i)=>{
b.disabled=true;
if(i===q.c)b.classList.add("correct");
else if(i===choice)b.classList.add("wrong");
});
document.getElementById("next").classList.remove("hidden");
document.getElementById("next").textContent=
questionIndex===item.questions.length-1?"Nəticəni gör →":"Növbəti sual →";
}
function nextQuestion(){
if(!locked)return;
const item=tests[sectionKey].items[testIndex];
if(questionIndex<item.questions.length-1){
questionIndex++;showQuestion();return;
}
history.push({section:tests[sectionKey].title,test:item.title,score:score,total:item.questions.length});
document.getElementById("progress").textContent="Test tamamlandı!";
document.getElementById("question").textContent="Well done! 🎉";
document.getElementById("answers").innerHTML="";
document.getElementById("feedback").textContent="";
document.getElementById("next").classList.add("hidden");
document.getElementById("finish").classList.remove("hidden");
document.getElementById("finalScore").textContent=
"Nəticən: "+score+" / "+item.questions.length+
" ("+Math.round(score/item.questions.length*100)+"%)";
}
function showResults(){
hideAll();
document.getElementById("results").classList.remove("hidden");
const list=document.getElementById("resultList");
list.innerHTML="";
if(!history.length){list.textContent="Hələ tamamlanmış test yoxdur. İlk testini et! 🌷";return;}
history.forEach((h,i)=>{
const p=document.createElement("p");
p.textContent=(i+1)+". "+h.test+" — "+h.score+"/"+h.total+" düzgün cavab";
list.appendChild(p);
});
}
</script>
</body>
</html>
