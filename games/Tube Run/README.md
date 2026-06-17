# 🌀 Tube Run

A reflex-based drag game where you navigate through a winding tube while dodging obstacles. Built with vanilla HTML, CSS, and JavaScript.

**[Play the Game](https://SwagataSarkar.github.io/tube-run)**

---

## 🎯 Game Overview

Drag from one green circle to the other through a winding tube. Stay centered, avoid obstacles, and don't touch the walls!

### Key Features

- **Bidirectional dragging** — start from either end
- **Two obstacle types** — stationary (weave around) and blinking (time your drag)
- **Progressive difficulty** — tube narrows every round
- **Real-time feedback** — live centeredness meter, collision warnings
- **Sound effects** — Web Audio API procedural sounds (toggle on/off)
- **High score tracking** — saved in your browser
- **Streak tracking** — consecutive successful runs
- **Touch + mouse support** — works on desktop and mobile

---

## 🎮 How to Play

1. **Drag** from either green circle through the winding tube
2. **Stay centered** — the closer to the center, the higher your accuracy score
3. **Avoid obstacles**:
   - Red **■ Stationary** blocks — weave around them
   - Orange **◉ Blinking** blocks — wait for them to disappear, then drag through
4. **Don't touch the walls** — instant fail!
5. **Complete the run** to see your score

### Scoring

- **80% Accuracy** — how centered you stayed in the tube
- **20% Speed** — how fast you completed the run
- **Bonus** — score ≥ 90 triggers a celebratory fanfare

### Difficulty

- Tube width starts at ~30px
- Narrows by ~0.8px every round (win or lose)
- Minimum width: 8px (extremely challenging!)
- More obstacles appear as you level up

---

## 🎵 Sound Effects

| Event | Sound |
|-------|-------|
| Start drag | `pop` — short chirp |
| Wall touch | `buzzer` — harsh sawtooth |
| Obstacle hit | `crash` — white noise burst |
| Reached the end | `complete` — soft, satisfying thump |
| Score 70-89 | `success` — rising arpeggio |
| Score 90+ | `ding` + `fanfare` |
| New high score | `fanfare` — celebratory jingle |

Click the **🔊/🔇** button to toggle sound on/off.

---

## 🛠️ Installation

### Option 1: Download the HTML file

1. Download `tube-run.html`
2. Open it in your browser
3. Start playing!

### Option 2: Clone the repository

```bash
git clone https://github.com/SwagataSarkar/SwagataSarkar.github.io.git
cd SwagataSarkar.github.io
open "games/Tube Run/tube-run.html"
```
