# 🧠 Memory Match

A polished, single-file browser game: memorize a shuffled board of cards, then find all the matching pairs. Built with plain HTML, CSS, and JavaScript — no installs, no dependencies, just open it and play.

## ✨ Features

- **Memorize phase** — every new game briefly flips all cards face-up for 10 seconds so you can study the board, then flips them back down and the clock starts on your first click.
- **Three difficulty levels** — 4×4 (Easy, 8 pairs), 6×6 (Medium, 18 pairs), and 8×8 (Hard, 32 pairs).
- **Two visual modes** — match by **Colors** (a 32-color palette) or by **Emoji** (animals, fruit, weather, hearts, and more).
- **Live stats bar** — tracks attempts, matches found, and elapsed time as you play.
- **Scoring & best-score tracking** — each win is scored out of 100 based on attempts and speed, with your best result per difficulty/mode saved locally in the browser so you can try to beat it.
- **Sound effects** — subtle procedurally-generated tones (via the Web Audio API) for flips, matches, mismatches, starting a round, and winning — toggle on/off with the speaker icon.
- **Keyboard shortcuts** — press `N` to start a new game, and `Space`/`Enter` to play again from the win screen.
- **Responsive layout** — scales down cleanly for smaller screens and mobile.

## 🎮 How to Play

1. Choose a difficulty and mode from the top controls.
2. Click **New Game** — all cards flip face-up for a few seconds so you can memorize their positions.
3. Once they flip back down, click any card to start the timer and begin matching pairs.
4. Click two cards at a time — matched pairs stay revealed, mismatches flip back over.
5. Match every pair to win and see your attempts, time, and score.

## 🚀 Getting Started

No build tools or server required.

1. Clone or download this repository
2. Open `memory-match.html` directly in any modern web browser

## 🛠️ Built With

- Plain HTML, CSS, and JavaScript (no frameworks or libraries)
- CSS Grid for the responsive board layout and 3D flip transforms for the cards
- The Web Audio API for all sound effects (synthesized on the fly, no audio files)
- `localStorage` for persisting best scores per difficulty and mode

## 📁 Project Structure

```
memory-match.html   # everything: markup, styles, and logic in one file
```

## 📄 License

Add a license of your choice here (e.g. MIT) before publishing.
