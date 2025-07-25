let round = 1;
let finishLine = 30;

let totalPlayers = 8;
let positions = new Array(totalPlayers).fill(0);
let currentPlayer = 0;

let activePlayers = [...Array(totalPlayers).keys()];

let round1Winners = [];
let round2Winners = [];
let finalWinner = null;

const roundDisplay = document.getElementById("round");
const currentPlayerDisplay = document.getElementById("currentPlayer");
const diceResultDisplay = document.getElementById("diceResult");
const playersDisplay = document.getElementById("players");
const winnerDisplay = document.getElementById("winner");
const rollBtn = document.getElementById("rollDice");
const restartBtn = document.getElementById("restartBtn");

function renderPlayers() {
  playersDisplay.innerHTML = "";
  activePlayers.forEach((playerIndex) => {
    const pos = positions[playerIndex];
    const p = document.createElement("p");
    p.className = "player";

    let winTag = "";
    if (round === 1 && round1Winners.includes(playerIndex)) winTag = " 🏁";
    if (round === 2 && round2Winners.includes(playerIndex)) winTag = " 🏁";
    if (round === 3 && finalWinner === playerIndex) winTag = " 👑";

    p.textContent = `O‘yinchi ${playerIndex + 1}: ${pos}-katak${winTag}`;
    playersDisplay.appendChild(p);
  });
}

function showRestartButton() {
  restartBtn.style.display = "inline-block";
}

function restartGame() {
  round = 1;
  finishLine = 30;
  totalPlayers = 8;
  positions = new Array(totalPlayers).fill(0);
  currentPlayer = 0;
  round1Winners = [];
  round2Winners = [];
  finalWinner = null;
  activePlayers = [...Array(totalPlayers).keys()];

  roundDisplay.textContent = round;
  diceResultDisplay.textContent = "-";
  winnerDisplay.textContent = "";
  currentPlayerDisplay.textContent = "1";
  restartBtn.style.display = "none";
  rollBtn.disabled = false;

  renderPlayers();
}

restartBtn.addEventListener("click", restartGame);

function resetForNextRound(newPlayers) {
  round++;
  roundDisplay.textContent = round;
  winnerDisplay.textContent = "";
  positions = new Array(totalPlayers).fill(0);
  activePlayers = [...newPlayers];
  currentPlayer = 0;
  rollBtn.disabled = false;
  renderPlayers();
}

function endRound1() {
  winnerDisplay.textContent = `✅ 1-bosqich yakunlandi! G‘oliblar: ${round1Winners.map(i => `O‘yinchi ${i + 1}`).join(', ')}. 2-bosqich boshlanmoqda...`;
  setTimeout(() => resetForNextRound(round1Winners), 3000);
}

function endRound2() {
  winnerDisplay.textContent = `✅ 2-bosqich yakunlandi! G‘oliblar: ${round2Winners.map(i => `O‘yinchi ${i + 1}`).join(', ')}. 3-bosqich boshlanmoqda...`;
  setTimeout(() => resetForNextRound(round2Winners), 3000);
}

function endRound3() {
  winnerDisplay.textContent = `🏆 Yakuniy G‘olib: O‘yinchi ${finalWinner + 1}! Tabriklaymiz!`;
  rollBtn.disabled = true;
  showRestartButton();
}

renderPlayers();

rollBtn.addEventListener("click", () => {
  if (rollBtn.disabled) return;

  const dice = Math.floor(Math.random() * 6) + 1;
  diceResultDisplay.textContent = dice;

  const playerIndex = activePlayers[currentPlayer];

  if (positions[playerIndex] >= finishLine) {
    currentPlayer = (currentPlayer + 1) % activePlayers.length;
    currentPlayerDisplay.textContent = activePlayers[currentPlayer] + 1;
    return;
  }

  positions[playerIndex] += dice;

  if (positions[playerIndex] >= finishLine) {
    positions[playerIndex] = finishLine;

    if (round === 1 && !round1Winners.includes(playerIndex)) {
      round1Winners.push(playerIndex);
      if (round1Winners.length === 3) {
        renderPlayers();
        endRound1();
        return;
      }
    }

    if (round === 2 && !round2Winners.includes(playerIndex)) {
      round2Winners.push(playerIndex);
      if (round2Winners.length === 2) {
        renderPlayers();
        endRound2();
        return;
      }
    }

    if (round === 3 && finalWinner === null) {
      finalWinner = playerIndex;
      renderPlayers();
      endRound3();
      return;
    }
  }

  renderPlayers();

  currentPlayer = (currentPlayer + 1) % activePlayers.length;
  currentPlayerDisplay.textContent = activePlayers[currentPlayer] + 1;
});
