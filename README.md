<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Find the Impostor</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #1c1c1c, #2e2e2e);
      color: #f1f1f1;
      padding: 30px;
    }
    .container {
      max-width: 700px;
      margin: auto;
      background: #252525;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.6);
    }
    h1, h2, h3 {
      text-align: center;
      color: #00c3ff;
    }
    label {
      display: block;
      margin-top: 15px;
      color: #ccc;
    }
    input {
      padding: 10px;
      width: 100%;
      margin-top: 5px;
      border-radius: 8px;
      border: none;
    }
    button {
      display: block;
      width: 100%;
      padding: 12px;
      margin-top: 20px;
      background: #00c3ff;
      color: white;
      font-size: 16px;
      font-weight: bold;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background 0.3s;
    }
    button:hover {
      background: #009ddc;
    }
    .question-box, .reveal-box {
      margin-top: 30px;
      display: none;
    }
    .player-question {
      background: #333;
      padding: 10px;
      border-radius: 10px;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Find the Impostor</h1>
    <label>Player 1 Name:</label>
    <input id="p1" type="text" />
    <label>Player 2 Name:</label>
    <input id="p2" type="text" />
    <label>Player 3 Name:</label>
    <input id="p3" type="text" />
    <button onclick="startGame()">Start Game</button><div class="question-box" id="questionBox">
  <h2>Player Questions (keep secret!):</h2>
  <div class="player-question" id="q1"></div>
  <div class="player-question" id="q2"></div>
  <div class="player-question" id="q3"></div>
  <button onclick="revealAnswers()">Reveal Answers</button>
</div>

<div class="reveal-box" id="revealBox">
  <h2>Answers:</h2>
  <p id="a1"></p>
  <p id="a2"></p>
  <p id="a3"></p>
  <h3>Who do you think is the impostor?</h3>
</div>

  </div>  <script>
    const similarPairs = [
      ["How many friends does the average person have?", "How many friends is too many in your opinion?"],
      ["How many hours of sleep do people usually get?", "How many hours of sleep do you personally need?"],
      ["How many countries are in Europe?", "How many countries do you want to visit?"],
      ["What is the average daily screen time?", "What is your daily screen time?"],
      ["What age do people usually get married?", "What age do you want to get married?"],
      ["What is a healthy number of steps per day?", "How many steps do you take per day?"]
    ];

    function getRandomPair() {
      return similarPairs[Math.floor(Math.random() * similarPairs.length)];
    }

    function startGame() {
      const players = [
        document.getElementById('p1').value || "Player 1",
        document.getElementById('p2').value || "Player 2",
        document.getElementById('p3').value || "Player 3"
      ];

      const imposterIndex = Math.floor(Math.random() * 3);
      const [commonQ, imposterQ] = getRandomPair();

      const questions = players.map((_, i) => i === imposterIndex ? imposterQ : commonQ);

      document.getElementById('q1').innerText = `${players[0]}: ${questions[0]}`;
      document.getElementById('q2').innerText = `${players[1]}: ${questions[1]}`;
      document.getElementById('q3').innerText = `${players[2]}: ${questions[2]}`;
      document.getElementById('questionBox').style.display = 'block';
    }

    function revealAnswers() {
      const a1 = prompt("Player 1, what is your answer?");
      const a2 = prompt("Player 2, what is your answer?");
      const a3 = prompt("Player 3, what is your answer?");

      document.getElementById('a1').innerText = `Player 1: ${a1}`;
      document.getElementById('a2').innerText = `Player 2: ${a2}`;
      document.getElementById('a3').innerText = `Player 3: ${a3}`;
      document.getElementById('revealBox').style.display = 'block';
    }
  </script></body>
</html>
