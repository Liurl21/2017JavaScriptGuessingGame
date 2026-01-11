
# JavaScript Guessing Game (Vanilla JS)

A small, single-page browser game: you pick a secret number (1–999) and the computer tries to guess it in **10 attempts**.

This project is intentionally “no framework / no build step” and is designed to showcase solid fundamentals: DOM manipulation, validation, event handling, and thoughtful UI/UX.

## Highlights (Recruiter-Friendly)

- **Vanilla JavaScript app structure**: logic moved out of HTML into [js/script.js](js/script.js) (separation of concerns).
- **Input validation + user feedback**: guards against non-numeric, non-integer, and out-of-range values with inline status messaging.
- **Accessible UI**: semantic labels, a live-updating status area (`role="status"` + `aria-live="polite"`), and keyboard-friendly form behavior.
- **Responsive, modern CSS**: CSS variables, `clamp()` typography, Grid/Flex layouts, focus rings, and `prefers-reduced-motion` support.
- **Clear “round log” output**: each guess is rendered as a styled log entry with contextual state (“Too low”, “Too high”, “Correct”).

## How to Play

1. Enter a whole number between **1** and **999**.
2. Click **Start guessing**.
3. The computer makes up to **10 guesses** and prints a round-by-round log.
4. If it guesses correctly within 10 tries, the computer wins; otherwise, you win.

## How It Works (Developer Notes)

The computer uses a **random guess within a shrinking range**:

- Start with `min = 1`, `max = 999`.
- Each guess picks a random integer in `[min, max]`.
- If the guess is too low → update `min = guess + 1`.
- If the guess is too high → update `max = guess - 1`.

This is not a pure binary search (by design). It demonstrates maintaining state across iterations and producing user-facing output each step.

### Key behaviors in the code

- **Validation**: `validateNumber(input)` ensures finite integer input in range.
- **Guess generation**: `guessNumber(minGuess, maxGuess)` returns an integer in the current bounds.
- **UI updates**:
  - `setMessage(kind, text)` / `clearMessage()` update the status banner.
  - `updateOutput(...)` appends a styled entry to the round log.
- **Event wiring**: listeners are attached on `DOMContentLoaded` and the form submit is intercepted to prevent full-page reload.

## Design / UI Implementation Notes

The UI was built to feel “portfolio-ready” while staying lightweight:

- **Consistent theme via CSS variables** (`:root` tokens for backgrounds, accents, and semantic colors).
- **Interactive affordances**: focus-visible ring, button hover/active states, and readable spacing.
- **Readable output layout**: log entries use a two-column grid (meta + numeric guess) with color-coded left borders.
- **Motion sensitivity**: transitions are disabled under `prefers-reduced-motion: reduce`.

## Run Locally

No build step.

- Option A: open [index.html](index.html) directly in your browser.
- Option B (recommended): serve as static files.
  - Any static server works (VS Code Live Server, `python -m http.server`, etc.).

## Project Structure

```
.
├─ index.html
├─ README.md
├─ css/
│  └─ myStyles.css
└─ js/
   └─ script.js
```

## Customization Ideas

- Change range: update the HTML input attributes, `validateNumber`, and the initial `guessMin/guessMax` values.
- Change attempt limit: update the loop limit in `guessingGame()` and the “used all guesses” check in `updateOutput()`.
- Swap strategy: replace the random-in-range guess with a deterministic mid-point guess to turn it into true binary search.

## Notes / Limitations

- Because guessing is random (within a narrowing range), the computer may occasionally fail within 10 tries even though it is narrowing the bounds.

