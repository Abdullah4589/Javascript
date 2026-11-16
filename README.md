# Terminal Slot Machine

A small Node.js program that runs a 3×3 slot machine in the terminal. You type a starting balance, pick how many lines to play, place a bet, and the program prints a spin and updates that balance.

The only purpose of this project is to learn JavaScript. It is practice: reading input, using functions, generating random results, and keeping a running total. It is not a product, and it is not meant to be used as a game for money.

The balance is a number in memory. No account is created, no payment is taken, and nothing here connects to real money.

## A clear stance on gambling

I do not gamble, and I do not support gambling. I am strictly against it, and I advise other people not to gamble either.

Real-money betting, casinos, and “just one more spin” products are built so the house keeps the advantage. Losses add up, and the habit is easy to slide into. This repository is not an invitation to do any of that. If you are looking for a place to wager money, this is the wrong project, and you should walk away from that idea entirely.

The code is here only as a way to learn JavaScript: input checks, a random draw, and a running total in one short script. Treat the dollar signs on screen as labels in a lesson, not as money.

## What you will see

Each spin prints three rows and three columns, for example:

```
A | C | D
B | B | B
D | C | A
```

You choose 1, 2, or 3 lines. Line 1 is the top row, line 2 is the middle row, and line 3 is the bottom row. A line wins only when all three symbols on that row are the same. The program then adds the payout to your balance and asks whether you want another spin. If the balance hits zero, the game ends.

## Symbols and payouts

Each reel is filled by drawing without replacement from this pool. Rarer symbols pay more.

| Symbol | Copies in the pool | Payout multiplier |
| ------ | -----------------: | ----------------: |
| A      |                  2 |                 5 |
| B      |                  4 |                 4 |
| C      |                  6 |                 3 |
| D      |                  8 |                 2 |

A winning line pays `bet per line × multiplier`. Betting on three lines costs `bet per line × 3` before the spin. The bet is rejected if that total is more than the current balance, or if the amount is not a number greater than zero.

## Requirements

- [Node.js](https://nodejs.org/) (current LTS is fine)
- npm, which ships with Node.js

## How to run

Clone the repository and install the one dependency (`prompt-sync`, used to read what you type):

```bash
git clone https://github.com/Abdullah4589/Javascript.git
cd Javascript
npm install
node project.js
```

If you already have this folder, `npm install` and `node project.js` are enough.

## Walkthrough of a session

1. **Deposit.** The program asks `Enter a deposit amount:`. Type a number greater than zero, such as `100`. Anything else is rejected and you are asked again. This only sets the starting balance for the session.
2. **Lines.** It asks `Enter the number of lines to bet on (1-3):`. Type `1`, `2`, or `3`.
3. **Bet.** It asks `Enter the bet per line :`. The amount must be greater than zero, and `bet × lines` must fit in the balance. That total is subtracted before the reels are drawn.
4. **Spin.** Three reels are built, turned into rows, and printed. Matching rows you paid for are scored with the table above.
5. **Result.** You see `You won, $...` (this is `0` when nothing matched). The payout is added back to the balance.
6. **Again or stop.** If the balance is zero, you see `You have no money left, game over.` Otherwise it asks `Do you want to play again? (y/n):`. `y` starts another spin with the same balance. Any other answer prints `Thank you for playing!` and exits.

Press `Ctrl+C` at any prompt to quit immediately. The balance is not saved.

## How the code is organized

Everything lives in [`project.js`](project.js):

| Function | Role |
| -------- | ---- |
| `deposit` | Reads a starting balance and rejects invalid numbers |
| `getNumberOfLines` | Reads 1, 2, or 3 |
| `getBet` | Reads a per-line bet that the balance can cover |
| `spin` | Builds three reels by random draws without replacement |
| `transpose` | Turns reels (columns) into the rows that get printed and scored |
| `printRows` | Prints the grid |
| `getWinnings` | Pays matching lines using `SYMBOL_VALUES` |
| `game` | Runs the loop until you stop or the balance is zero |

`SYMBOLS_COUNT` and `SYMBOL_VALUES` at the top of the file are the only places that define the pool and the payouts.

## License

ISC. See [`package.json`](package.json).
