<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Quiz por Categoria</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #111;
      color: #fff;
      text-align: center;
      padding: 20px;
    }
    .box {
      max-width: 400px;
      margin: auto;
      background: #222;
      border-radius: 12px;
      padding: 20px;
      box-shadow: 0 0 10px #000;
    }
    .btn {
      display: block;
      background: #333;
      border: none;
      color: #fff;
      padding: 10px;
      margin: 10px auto;
      width: 90%;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.3s;
    }
    .btn:hover {
      background: #444;
    }
    .result {
      font-size: 24px;
      margin-top: 20px;
    }
  </style>
</head>
<body>
  <div class="box" id="menu">
    <h2>Escolha a Categoria</h2>
    <button class="btn" onclick="startQuiz('animes')">Animes</button>
    <button class="btn" onclick="startQuiz('jogos')">Jogos</button>
    <button class="btn" onclick="startQuiz('escola')">Escola</button>
  </div>

  <div class="box" id="quiz" style="display:none;">
    <h2 class="question">Pergunta aqui</h2>
    <div id="answers"></div>
    <div class="result" id="result"></div>
  </div>

  <script>
    const perguntas = {
      animes: [
        { question: "Qual é o personagem principal de One Piece?", options: ["Zoro", "Naruto", "Luffy", "Goku"], answer: "Luffy" },
        { question: "Em Naruto, quem é o rival do Naruto?", options: ["Sasuke", "Kakashi", "Shikamaru", "Gaara"], answer: "Sasuke" }
        { question: "Qual é o nome do anime de romanve que tem uma coelhinha", options : ["Naruto","One piece","Bunny grilt senpai"], answer: "Bunnu grilt senpai" }
      ],
      jogos: [
        { question: "Quem criou o Free Fire?", options: ["Garena", "Riot", "Epic Games", "Tencent"], answer: "Garena" },
        { question: "Qual é o jogo mais vendido da história?", options: ["Minecraft", "GTA V", "FIFA", "Fortnite"], answer: "Minecraft" }
      ],
      escola: [
        { question: "Qual a capital do Brasil?", options: ["São Paulo", "Brasília", "Rio de Janeiro", "Recife"], answer: "Brasília" },
        { question: "2 + 2 = ?", options: ["3", "4", "5", "2"], answer: "4" }
      ]
    };

    let categoriaAtual = '';
    let questoes = [];
    let current = 0;
    let score = 0;

    function startQuiz(categoria) {
      categoriaAtual = categoria;
      questoes = perguntas[categoria];
      current = 0;
      score = 0;
      document.getElementById("menu").style.display = "none";
      document.getElementById("quiz").style.display = "block";
      showQuestion();
    }

    function showQuestion() {
      const q = questoes[current];
      document.querySelector(".question").textContent = q.question;
      const answersEl = document.getElementById("answers");
      answersEl.innerHTML = "";
      q.options.forEach(opt => {
        const btn = document.createElement("button");
        btn.textContent = opt;
        btn.className = "btn";
        btn.onclick = () => checkAnswer(opt);
        answersEl.appendChild(btn);
      });
    }

    function checkAnswer(selected) {
      if (selected === questoes[current].answer) {
        score++;
      }
      current++;
      if (current < questoes.length) {
        showQuestion();
      } else {
        showResult();
      }
    }

    function showResult() {
      document.querySelector(".question").style.display = "none";
      document.getElementById("answers").style.display = "none";
      document.getElementById("result").innerHTML = `
        Você acertou <strong>${score}</strong> de <strong>${questoes.length}</strong> perguntas!<br><br>
        <button class="btn" onclick="restart()">Voltar ao Menu</button>
      `;
    }

    function restart() {
      document.querySelector(".question").style.display = "block";
      document.getElementById("answers").style.display = "block";
      document.getElementById("result").innerHTML = "";
      document.getElementById("quiz").style.display = "none";
      document.getElementById("menu").style.display = "block";
    }
  </script>
</body>
</html>


