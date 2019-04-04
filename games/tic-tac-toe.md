# Tic-Tac-Toe

Let's build [tic-tac-toe](https://en.wikipedia.org/wiki/Tic-tac-toe).

## Structure

A tic-tac-toe game has a few layers:

- The input layer
- The game layer
- The board layer
- The display layer

Each layer will require multiple classes, objects, and functions.  It's up to you to decide how to organize it.

The input layer is responsible for gather input, whether from a human typing on a keyboard, from a computer-controlled player, a file consisting of moves, or anywhere else.

The game layer is responsible for keeping track of which player's turn it is, whether one player has won, whether a player's chosen move is legal, etc.

The board layer is responsible for keeping track of what is on the board.

The display layer is responsible for displaying the current state of the board.

## Iterations

### v0.1 - Board + Display

Don't worry about the game yet.  Start by writing code that can manage the board and display boards.

- [ ] Implement a board that represents a 3x3 tic-tac-toe game.
- [ ] Create an interface (in code) that allows placement of characters on the board.
- [ ] Handle error cases (e.g., someone trying to overwrite a square, someone trying to place something out of bounds)
- [ ] Write code that takes a board and prints out a human-friendly display
- [ ] Write driver code that fills up an example board or two and displays them

### v0.2 - Game Layer

Add a layer that includes logic about the game, including:

- Players
- The state of the game (whose turn is it, has anyone won)

Do not worry about getting user input yet.  Instead, have your code play a game "by hand" by hard-coding placements that lead to specific game states (win, lose, draw).

For example, maybe the code looks like the following.  This is only a suggestion — you decide how to organize the code for the game!

```javascript
const playerX = new Player('X');
const playerO = new Player('O');

const game = new Game(players: [playerX, playerO]);

game.takeTurn(playerX, [0, 0]);
game.takeTurn(playerO, [1, 1]);

printBoard(game.board);

// Prints out:
//
// |X| | |
// | |O| |
// | | | |
```

### v1.0 - Input Layer

Create an interactive version that lets two people at the same keyboard take turns playing until one player wins or there is a draw.
