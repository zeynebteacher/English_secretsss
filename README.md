
<!DOCTYPE html>
<html lang="az">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>English Secret</title>
<style>
body {
  font-family: Arial, sans-serif;
  background: #f7f1e8;
  color: #39312d;
  margin: 0;
  padding: 20px;
}
header {
  text-align: center;
  background: #d9c3a5;
  padding: 25px;
  border-radius: 16px;
}
h1 { color: #49382e; }
main {
  max-width: 700px;
  margin: 25px auto;
}
.card {
  background: white;
  padding: 20px;
  margin: 15px 0;
  border-radius: 14px;
  box-shadow: 0 2px 8px #00000012;
}
button {
  background: #80634d;
  color: white;
  border: none;
  padding: 12px 18px;
  border-radius: 8px;
  cursor: pointer;
  margin: 5px;
}
button:hover { background: #604832; }
input {
  padding: 10px;
  width: 90%;
  margin: 6px 0;
}
</style>
</head>
<body>

<header>
  <h1>English Secret</h1>
  <p>Learn English. Test yourself. Improve every day!</p>
</header>

<main>
  <div class="card">
    <h2>Şagird girişi</h2>
    <p>Adını daxil et və sınağa başla.</p>
    <input id="studentName" type="text" placeholder="Ad və soyad">
    <br>
    <button onclick="startTest()">Sınağa başla</button>
    <p id="welcome"></p>
  </div>

  <div class="card">
    <h2>İngilis dili sınağı</h2>
    <p id="question">Başlamaq üçün adını daxil et.</p>
    <div id="answers"></div>
    <p id="result"></p>
    <button onclick="nextQuestion()">Növbəti sual</button>
  </div>
</main>

<script>
const questions = [
  {
    q: "Choose the correct answer: She ___ to school every day.",
    options: ["go", "goes", "going", "gone"],
    answer: 1
  },
  {
    q: "What is the plural of 'child'?",
    options: ["childs", "childes", "children", "childrens"],
    answer: 2
  },
  {
    q: "Choose the synonym of 'happy'.",
    options: ["sad", "glad", "angry", "tired"],
    answer: 1
  },
  {
    q: "They ___ watching TV now.",
    options: ["is", "am", "are", "be"],
    answer: 2
  },
  {
    q: "What is the opposite of 'difficult'?",
    options: ["easy", "hard", "strong", "late"],
    answer: 0
  }
];

let current = 0;
let score = 0;
let selected = false;

function startTest() {
  const name = document.getElementById("studentName").value.trim();
  document.getElementById("testBox").style.display = "block";

  if (!name) {
    alert("Zəhmət olmasa adını daxil et.");
    return;
  }

  document.getElementById("welcome").textContent =
    "Uğurlar, " + name + "!";

  current = 0;
  score = 0;
  showQuestion();
}

function showQuestion() {
  if (current >= questions.length) {
    document.getElementById("question").textContent =
      "Sınaq tamamlandı!";
    document.getElementById("answers").innerHTML = "";
    document.getElementById("result").textContent =
      "Nəticən: " + score + " / " + questions.length;
    return;
  }

  selected = false;
  document.getElementById("result").textContent = "";
  document.getElementById("question").textContent =
    (current + 1) + ". " + questions[current].q;

  let html = "";

  questions[current].options.forEach(function(option, index) {
    html += '<p><button onclick="checkAnswer(' + index + ')">' +
      option + '</button></p>';
  });

  document.getElementById("answers").innerHTML = html;
}

function checkAnswer(index) {
  if (selected) return;
  selected = true;

  if (index === questions[current].answer) {
    score++;
    document.getElementById("result").textContent = "Düzgün cavab! 🎉";
  } else {
    document.getElementById("result").textContent =
      "Səhv cavab. Düzgün cavab: " +
      questions[current].options[questions[current].answer];
  }
}

function nextQuestion() {
  if (current >= questions.length) return;

  if (!selected) {
    alert("Əvvəl cavab variantını seç.");
    return;
  }

  current++;
  showQuestion();
}
</script>

</body>
</html>
