I have created a ZIP-ready project for your Tic Tac Toe game. You can copy this content into a ZIP file:

---

**Folder structure:**

```
tic-tac-toe/
+-- index.html
+-- README.md
```

**index.html:**

```html
<!DOCTYPE html>
<html>
<head>
<title>Tic Tac Toe</title>

<style>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background: #f2f2f2;
}
.board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    gap: 5px;
    justify-content: center;
    margin-top: 20px;
}
.cell {
    width: 100px;
    height: 100px;
    font-size: 40px;
    cursor: pointer;
    background: white;
    border: 2px solid black;
}
button, select {
    margin-top: 10px;
    padding: 8px 15px;
    font-size: 16px;
}
#status {
    margin-top: 10px;
    font-size: 18px;
}
</style>
</head>

<body>

<h1>Tic Tac Toe</h1>
<p>Developer: <b>Ansh More</b></p>

<select id="mode">
    <option value="pvp">Player vs Player</option>
    <option value="ai">Player vs Computer</option>
</select>

<div class="board">
    <button class="cell" onclick="play(0)"></button>
    <button class="cell" onclick="play(1)"></button>
    <button class="cell" onclick="play(2)"></button>
    <button class="cell" onclick="play(3)"></button>
    <button class="cell" onclick="play(4)"></button>
    <button class="cell" onclick="play(5)"></button>
    <button class="cell" onclick="play(6)"></button>
    <button class="cell" onclick="play(7)"></button>
    <button class="cell" onclick="play(8)"></button>
</div>

<div id="status">Player X turn</div>
<button onclick="resetGame()">Restart</button>

<script>
let board = ["","","","","","","","",""];
let currentPlayer = "X";
let gameOver = false;

const winPatterns = [
    [0,1,2],[3,4,5],[6,7,8],
    [0,3,6],[1,4,7],[2,5,8],
    [0,4,8],[2,4,6]
];

function play(i) {
    if (board[i] !== "" || gameOver) return;

    board[i] = currentPlayer;
    document.getElementsByClassName("cell")[i].innerText = currentPlayer;

    if (checkWin(currentPlayer)) {
        document.getElementById("status").innerText = currentPlayer + " wins!";
        gameOver = true;
        return;
    }

    if (!board.includes("")) {
        document.getElementById("status").innerText = "Draw!";
        gameOver = true;
        return;
    }

    currentPlayer = currentPlayer === "X" ? "O" : "X";
    document.getElementById("status").innerText = "Player " + currentPlayer + " turn";

    if (document.getElementById("mode").value === "ai" && currentPlayer === "O") {
        setTimeout(aiMove, 500);
    }
}

function aiMove() {
    let move = findBestMove("O") || findBestMove("X") || randomMove();
    play(move);
}

function findBestMove(player) {
    for (let p of winPatterns) {
        let v = p.map(i => board[i]);
        if (v.filter(x => x === player).length === 2 && v.includes(""))
            return p[v.indexOf("")];
    }
    return null;
}

function randomMove() {
    let empty = board.map((v,i)=>v===""?i:null).filter(v=>v!==null);
    return empty[Math.floor(Math.random()*empty.length)];
}

function checkWin(player) {
    return winPatterns.some(p => p.every(i => board[i] === player));
}

function resetGame() {
    board = ["","","","","","","","",""];
    gameOver = false;
    currentPlayer = "X";
    document.getElementById("status").innerText = "Player X turn";
    for (let c of document.getElementsByClassName("cell")) c.innerText="";
}
</script>

</body>
</html>
```

**README.md:**

```md
# Tic Tac Toe Game ??

A simple Tic Tac Toe game built using HTML, CSS, and JavaScript.

## Features
- Player vs Player
- Player vs Computer (AI)
- Clean and simple UI
- Works offline
- Free to play

## Developer
Ansh More

## Play the Game
After publishing on GitHub Pages, open:
https://YOUR-USERNAME.github.io/tic-tac-toe/
```





