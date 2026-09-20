
# 🎮 Tic Tac Toe Game

A simple and interactive **Tic Tac Toe** game built using **HTML, CSS, and JavaScript**.

This project is beginner-friendly and demonstrates how JavaScript can be used to handle user interactions, player turns, winning conditions, draw detection, and game reset functionality.

## 🚀 Live Demo

🔗 **Live Demo:** `https://github.com/parthsaradava/Tic-Tac-Toe.git`

---

## 📸 Preview

![Tic Tac Toe Preview](./screenshot.png)

---

## 🛠️ Technologies Used

* **HTML5** – Used to create the structure of the game.
* **CSS3** – Used to style the game board, buttons, and messages.
* **JavaScript** – Used to implement the game logic and user interactions.

---

## 🎯 Features

* 🎮 Two-player Tic Tac Toe game
* 🟢 Player O
* 🔴 Player X
* 🏆 Automatically detects the winner
* 🤝 Automatically detects a draw
* 🔒 Disables a box after it has been selected
* 🔄 New Game button
* ♻️ Reset Game button
* 📢 Displays the winner message
* 📢 Displays the draw message
* 🔁 Automatically resets the game after a draw

---

## 📂 Project Structure

```text
tic-tac-toe/
│
├── index.html
├── style.css
├── app.js
├── screenshot.png
└── README.md
```

---

## 🧠 How the Game Works

### 1. Selecting the Boxes

JavaScript first selects all the game boxes from the HTML:

```javascript
let boxes = document.querySelectorAll(".Box");
```

Then an event listener is added to every box:

```javascript
boxes.forEach((box) => {
  box.addEventListener("click", () => {
    // Game logic
  });
});
```

This allows the game to detect when a player clicks on a box.

---

### 2. Switching Between Players

The game uses a variable called `turnO` to keep track of whose turn it is:

```javascript
let turnO = true;
```

If `turnO` is `true`, Player O gets the turn.

If `turnO` is `false`, Player X gets the turn.

```javascript
if (turnO) {
  box.innerText = "O";
  box.style.color = "green";
  turnO = false;
} else {
  box.innerText = "X";
  box.style.color = "red";
  turnO = true;
}
```

After every move, the turn changes to the other player.

---

### 3. Disabling a Selected Box

After a player selects a box, that box is disabled:

```javascript
box.disabled = true;
```

This prevents players from changing an already selected box.

---

## 🏆 Winner Detection

The game contains all possible winning combinations:

```javascript
const winpatterns = [
  [0, 1, 2],
  [0, 3, 6],
  [0, 4, 8],
  [1, 4, 7],
  [2, 5, 8],
  [2, 4, 6],
  [3, 4, 5],
  [6, 7, 8],
];
```

The board can be represented like this:

```text
  0 | 1 | 2
 ---+---+---
  3 | 4 | 5
 ---+---+---
  6 | 7 | 8
```

For example:

```javascript
[0, 1, 2]
```

represents the first row.

And:

```javascript
[0, 3, 6]
```

represents the first column.

The `checkWinner()` function checks each possible winning combination:

```javascript
const checkWinner = () => {
  for (let pattern of winpatterns) {
    let pos1val = boxes[pattern[0]].innerText;
    let pos2val = boxes[pattern[1]].innerText;
    let pos3val = boxes[pattern[2]].innerText;

    if (pos1val != "" && pos2val != "" && pos3val != "") {
      if (pos1val === pos2val && pos2val === pos3val) {
        showWinner(pos1val);
        return;
      }
    }
  }

  checkDraw();
};
```

If all three positions contain the same value, that player wins.

---

## 🤝 Draw Detection

A draw happens when:

1. Nobody has won.
2. All 9 boxes are filled.

The game checks for a draw using the `checkDraw()` function:

```javascript
const checkDraw = () => {
  let allFilled = true;

  for (let box of boxes) {
    if (box.innerText === "") {
      allFilled = false;
      break;
    }
  }

  if (allFilled) {
    showDraw();
  }
};
```

The game first checks for a winner.

If nobody wins, it checks whether all boxes are filled:

```text
Player makes a move
        ↓
   Check Winner
        ↓
   Someone won?
     /       \
   Yes        No
   ↓           ↓
Winner     Check Draw
             ↓
       All boxes filled?
         /         \
       Yes          No
       ↓             ↓
     Draw       Continue Game
```

This is important because the final move could either create a winner or result in a draw.

---

## 🔄 Resetting the Game

The `resetGame()` function starts a new game:

```javascript
const resetGame = () => {
  turnO = true;
  enableBoxes();
  msgcontainer.classList.add("hide");
};
```

It performs three things:

* Sets the first turn back to O.
* Enables all boxes.
* Hides the result message.

---

## 🔁 Enable Boxes

The `enableBoxes()` function clears the previous game:

```javascript
const enableBoxes = () => {
  for (let box of boxes) {
    box.disabled = false;
    box.innerText = "";
  }
};
```

This allows players to start a new game.

---

## 🚫 Disable Boxes

The `disableBoxes()` function disables all boxes:

```javascript
const disableBoxes = () => {
  for (let box of boxes) {
    box.disabled = true;
  }
};
```

This is used when a player wins so that players cannot continue playing after the game has ended.

---

## 🏆 Showing the Winner

When a player wins, the `showWinner()` function displays the result:

```javascript
const showWinner = (winner) => {
  msg.innerText = `Congratulations, winner is ${winner}`;
  msgcontainer.classList.remove("hide");
  disableBoxes();
};
```

The game displays a message such as:

```text
Congratulations, winner is O
```

or:

```text
Congratulations, winner is X
```

---

## 🤝 Showing a Draw

When the game ends in a draw:

```javascript
const showDraw = () => {
  msg.innerText = "Game is a draw!";
  msgcontainer.classList.remove("hide");

  setTimeout(() => {
    resetGame();
  }, 1500);
};
```

The game displays:

```text
Game is a draw!
```

After **1.5 seconds**, the game automatically resets and a new game begins.

---

## ▶️ How to Run the Project

### Run Locally

1. Clone this repository:

```bash
git clone https://github.com/parthsaradava/Tic-Tac-Toe.git
```

2. Open the project folder.

3. Open `index.html` in your web browser.

4. Start playing! 🎮

---

## 🌐 GitHub Pages

This project can also be hosted using **GitHub Pages**.

After enabling GitHub Pages for the repository, you can access the game through your GitHub Pages URL.

Example:

```text
https://github.com/parthsaradava/Tic-Tac-Toe.git
```

---

## 📚 What I Learned

While creating this project, I practiced:

* HTML5
* CSS3
* JavaScript
* DOM manipulation
* `querySelectorAll()`
* Event listeners
* Arrays
* Loops
* Functions
* Conditional statements
* `if...else`
* Game logic
* Winner detection
* Draw detection
* Enabling and disabling HTML elements
* Updating HTML content using JavaScript
* Using `setTimeout()`

---

## 👨‍💻 Author

GitHub: `Parthsaradava`

---

## ⭐ Support

If you like this project, consider giving the repository a ⭐ **star** on GitHub!

Thank you for checking out my Tic Tac Toe project! 🎮


