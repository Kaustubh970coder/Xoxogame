# Xoxogame
Free game for cure booredom 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tic Tac Toe</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      text-align: center;
      margin-top: 50px;
      background: linear-gradient(135deg, #f0f8ff, #e6e6fa);
      color: #333;
    }

    h1 {
      color: #4b0082;
      font-size: 3rem;
      text-shadow: 2px 2px #ccc;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 10px;
      justify-content: center;
      margin: 30px auto;
    }

    .cell {
      background: #ffffff;
      border: none;
      border-radius: 15px;
      font-size: 2.5rem;
      font-weight: bold;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      transition: background 0.3s, transform 0.2s;
    }

    .cell:hover {
      background: #f0f0f0;
      transform: scale(1.05);
    }

    .cell.x {
      color: #ff4500;
    }

    .cell.o {
      color: #1e90ff;
    }

    #status {
      font-size: 1.5rem;
      margin-top: 20px;
      font-weight: bold;
    }

    #resetBtn {
      margin-top: 25px;
      padding: 10px 25px;
      font-size: 1rem;
      border: none;
      background: linear-gradient(135deg, #6a5acd, #8a2be2);
      color: white;
      border-radius: 10px;
      cursor: pointer;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
      transition: background 0.3s, transform 0.2s;
    }

    #resetBtn:hover {
      background: linear-gradient(135deg, #836fff, #7b68ee);
      transform: scale(1.05);
    }
  </style>
</head>
<body>
  <h1>Tic Tac Toe</h1>
  <div class="board" id="board">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
  </div>
  <div id="status">Current Player: X</div>
  <button id="resetBtn">Reset Game</button>

  <script>
    const cells = document.querySelectorAll('.cell');
    const statusText = document.getElementById('status');
    const resetBtn = document.getElementById('resetBtn');

    let currentPlayer = 'X';
    let board = ["", "", "", "", "", "", "", "", ""];
    let gameActive = true;

    const winConditions = [
      [0,1,2], [3,4,5], [6,7,8],
      [0,3,6], [1,4,7], [2,5,8],
      [0,4,8], [2,4,6]
    ];

    function handleClick(e) {
      const index = e.target.getAttribute('data-index');
      if (board[index] !== "" || !gameActive) return;

      board[index] = currentPlayer;
      e.target.textContent = currentPlayer;
      e.target.classList.add(currentPlayer.toLowerCase());

      if (checkWin()) {
        statusText.textContent = `Player ${currentPlayer} Wins!`;
        gameActive = false;
        return;
      }

      if (!board.includes("")) {
        statusText.textContent = "It's a Draw!";
        gameActive = false;
        return;
      }

      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      statusText.textContent = `Current Player: ${currentPlayer}`;
    }

    function checkWin() {
      return winConditions.some(condition => {
        const [a, b, c] = condition;
        return board[a] && board[a] === board[b] && board[a] === board[c];
      });
    }

    function resetGame() {
      board = ["", "", "", "", "", "", "", "", ""];
      currentPlayer = 'X';
      gameActive = true;
      statusText.textContent = `Current Player: ${currentPlayer}`;
      cells.forEach(cell => {
        cell.textContent = "";
        cell.classList.remove("x", "o");
      });
    }

    cells.forEach(cell => cell.addEventListener('click', handleClick));
    resetBtn.addEventListener('click', resetGame);
  </script>
</body>
</html>
