# JavaScript Guessing Game

A small, single-page JavaScript project where you secretly choose a number and the computer tries to guess it in **10 tries or fewer**.

This is a simple HTML/CSS/JavaScript exercise focused on:

- Validating user input
- Basic control flow (loops + conditionals)
- Random number generation
- Updating the DOM with game output

## How To Play

1. Enter a whole number between **1** and **999** (inclusive).
2. Click **Submit**.
3. The computer will make up to **10 guesses**.
4. For each guess, the game compares the guess to your number and prints whether the guess was **too low** or **too high**.
5. If the computer guesses correctly within 10 tries, it wins. Otherwise, you win.

## How It Works

The game keeps track of a shrinking range of possible answers:

- Starts with `min = 1` and `max = 999`
- Each time it guesses:
	- If the guess is too low, it updates `min = guess + 1`
	- If the guess is too high, it updates `max = guess - 1`

Each new guess is chosen randomly within the current `[min, max]` range.

### Input Validation

Your input is checked before the game runs:

- Must be a number
- Must be between 1 and 999 (inclusive)

If validation fails, the game shows an alert explaining what was wrong.

## Running Locally

This project is static (no build step).

Option A — open directly:

- Open `index.html` in a web browser.

Option B — serve with a simple local web server (recommended for consistent browser behavior):

- Use any basic static file server and navigate to the served page.

## Project Structure

```
.
├─ index.html
├─ README.md
└─ css/
	 └─ myStyles.css
```

## Files Of Interest

- `index.html`
	- Contains the HTML UI and the JavaScript game logic (inline `<script>`).
	- Key functions:
		- `validateNumber(input)` — checks user input is numeric and within range.
		- `guessNumber(minGuess, maxGuess)` — returns a random integer within the current bounds.
		- `updateOutput(...)` — appends a new result message to the output area.
		- `guessingGame()` — orchestrates the full game loop (up to 10 guesses).

- `css/myStyles.css`
	- Minimal styling for layout/centering.

## Customization

Common tweaks you can make:

- Change the allowed range:
	- Update the validation rules in `validateNumber`.
	- Update the initial bounds in `guessingGame` (`guessMin`, `guessMax`).

- Change number of guesses:
	- Update the loop limit in `guessingGame`.
	- Update the “win/lose” check in `updateOutput`.

## Notes / Limitations

- The guessing strategy is **random within a narrowing range** (not a true binary search), so it may sometimes fail to guess within 10 tries even though it is narrowing the bounds.
- Input is read from a text field; the validation step prevents values outside 1–999.

