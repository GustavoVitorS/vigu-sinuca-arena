# VIGU Sinuca Arena 🎱

A pool game with rules inspired by 8-ball, built using **HTML, CSS, and vanilla JavaScript**—no frameworks or external dependencies. It is designed to run directly in the browser and be hosted for free on **GitHub Pages**.

## Features

- Pool table rendered using `<canvas>`.
- Physics for balls, collisions, friction, cushions, and pockets.
- Aiming via mouse and touch.
- Gesture-based shots: hold, pull the cue back, and release.
- Shot power is proportional to the pull-back distance.
- CPU opponent with four difficulty levels:
- Easy
- Medium
- Hard
- HARDCORE
- HARDCORE mode unlocks only after winning a match at each of the three initial levels.
- Progress saved in the browser's `localStorage`.
- Responsive interface for desktop, tablet, and mobile.
- Custom sound effects for shots, collisions, cushion bounces, pocketing, victory, and defeat.
- 100% static project, ideal for GitHub Pages.

## Controls

- **Desktop:** Move the mouse to aim. Click and hold on the table, drag in the direction opposite to your aim to pull back the cue, and release to shoot.
- **Mobile/Tablet:** Tap in the direction you want to aim, hold your finger down, drag backward, and release.
- A quick click or tap simply adjusts the aim without accidentally firing a shot.

## How to play locally

Simply open `index.html` in your browser.

To avoid restrictions in some browsers, you can also run a local server:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080`.

## Publishing to GitHub Pages

1. Create a GitHub repository, e.g., `vigu-sinuca-arena`.
2. Push the project files to the `main` branch.
3. In the repository, go to **Settings → Pages**. 4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select the `main` branch and the `/ (root)` folder.
6. Click **Save**.
7. After a few moments, GitHub will display the game's public URL.

## Note on the rules

The game follows a simplified version of 8-ball rules, suitable for quick matches against the CPU:

- The first valid ball pocketed determines solids vs. stripes.
- After clearing your group, you must pocket the 8-ball.
- Pocketing the 8-ball prematurely results in a loss.
- Pocketing the cue ball results in a foul, and it is automatically placed back on the table.

## Structure

```text
vigu-sinuca-arena/
├── index.html
├── style.css
├── script.js
├── sounds/
│   ├── cue.wav
│   ├── collision.wav
│   ├── rail.wav
│   ├── pocket.wav
│   ├── ui.wav
│   ├── win.wav
│   └── lose.wav
└── README.md
```

## License

You may use, modify, and publish this project on your GitHub.
