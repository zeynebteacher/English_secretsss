<!DOCTYPE html>
<html lang="az">
<head>
  <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>English Secret</title>
        <style>
            body {
                      margin: 0;
                            font-family: Arial, sans-serif;
                                  background: #f8f2e9;
                                        color: #46392f;
                                              text-align: center;
            }
                header {
                          background: #e7d5c0;
                                padding: 30px 15px;
                }
                    h1 { font-size: 34px; }
                        main {
                                  max-width: 600px;
                                        margin: 30px auto;
                                              padding: 20px;
                        }
                            .card {
                                      background: white;
                                            padding: 22px;
                                                  margin: 18px 0;
                                                        border-radius: 16px;
                                                              box-shadow: 0 3px 12px #00000010;
                            }
                                button {
                                          background: #8b6b50;
                                                color: white;
                                                      border: 0;
                                                            border-radius: 9px;
                                                                  padding: 12px 20px;
                                                                        font-size: 16px;
                                                                              cursor: pointer;
                                }
                                    select {
                                              padding: 10px;
                                                    margin: 10px;
                                                          border-radius: 8px;
                                    }
                                        #result { font-weight: bold; }
                                          </style>
                                          </head>
                                          <body>
                                            <header>
                                                <h1>English Secret ✨</h1>
                                                    <p>Learn English step by step!</p>
                                                      </header>

                                                        <main>
                                                            <div class="card">
                                                                  <h2>Welcome, learner! 🤍</h2>
                                                                        <p>İngilis dilini bizimlə öyrən!</p>
                                                                            </div>

                                                                                <div class="card">
                                                                                      <h2>English Test</h2>
                                                                                            <p>Mövzu seç və biliyini yoxla.</p>
                                                                                                  <select id="topic" onchange="showQuestion()">
                                                                                                          <option value="present">Present Simple</option>
                                                                                                                  <option value="tobe">Verb to be</option>
                                                                                                                          <option value="vocab">Basic Vocabulary</option>
                                                                                                                                </select>
                                                                                                                                      <p id="question">She ___ to school every day.</p>
                                                                                                                                            <div id="answers"></div>
                                                                                                                                                  <p id="result"></p>
                                                                                                                                                      </div>
                                                                                                                                                        </main>

                                                                                                                                                          <script>
                                                                                                                                                              const tests = {
                                                                                                                                                                      present: {
                                                                                                                                                                                q: "She ___ to school every day.",
                                                                                                                                                                                        a: ["go", "goes", "going"],
                                                                                                                                                                                                correct: 1
                                                                                                                                                                      },
                                                                                                                                                                            tobe: {
                                                                                                                                                                                        q: "They ___ students.",
                                                                                                                                                                                                a: ["am", "is", "are"],
                                                                                                                                                                                                        correct: 2
                                                                                                                                                                            },
                                                                                                                                                                                  vocab: {
                                                                                                                                                                                            q: "What is the meaning of 'apple'?",
                                                                                                                                                                                                    a: ["Alma", "Kitab", "Masa"],
                                                                                                                                                                                                            correct: 0
                                                                                                                                                                                  }
                                                                                                                                                              };

                                                                                                                                                                  function showQuestion() {
                                                                                                                                                                          const test = tests[document.getElementById("topic").value];
                                                                                                                                                                                document.getElementById("question").textContent = test.q;
                                                                                                                                                                                      document.getElementById("result").textContent = "";
                                                                                                                                                                                            const area = document.getElementById("answers");
                                                                                                                                                                                                  area.innerHTML = "";
                                                                                                                                                                                                        test.a.forEach((answer, i) => {
                                                                                                                                                                                                                    const button = document.createElement("button");
                                                                                                                                                                                                                            button.textContent = answer;
                                                                                                                                                                                                                                    button.style.margin = "5px";
                                                                                                                                                                                                                                            button.onclick = () => {
                                                                                                                                                                                                                                                          document.getElementById("result").textContent =
                                                                                                                                                                                                                                                                      i === test.correct ? "Correct! 🎉" : "Try again! 💛";
                                                                                                                                                                  };
                                                                                                                                                                          area.appendChild(button);
                                                                                                                                                                  });
                                                                                                                                                                  }
                                                                                                                                                                      showQuestion();
                                                                                                                                                                        </script>
                                                                                                                                                                        </body>
                                                                                                                                                                        </html>
                                                                                                                                                                      }
            }