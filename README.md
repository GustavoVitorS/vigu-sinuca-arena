# VIGU Sinuca Arena 🎱

A pool game inspired by 8-ball rules, built with **HTML, CSS, and vanilla JavaScript**, with no frameworks or external dependencies. It was designed to run directly in the browser and to be published for free using **GitHub Pages**.

## Features

- Pool table rendered with `<canvas>`.
- Ball physics with collisions, friction, cushions, and pockets.
- Mouse and touch aiming.
- Gesture-based shots: hold, pull the cue back, and release.
- Shot power is proportional to the pull-back distance.
- CPU opponent with four difficulty levels:
  - Easy
  - Medium
  - Hard
  - HARDCORE
- HARDCORE mode is unlocked only after winning one match in each of the three initial difficulty levels.
- Progress is saved in the browser using `localStorage`.
- Responsive interface for desktop, tablet, and mobile.
- Custom sound effects for cue shots, collisions, cushion impacts, pocketing, victory, and defeat.
- 100% static project, ideal for GitHub Pages.

## Controls

- **Desktop:** move the mouse to aim. Click and hold on the table, drag in the opposite direction of the aim to pull the cue back, then release to shoot.
- **Mobile/tablet:** touch and hold outside the cue pull zone, then move your finger to adjust the aim continuously. To shoot, touch the cue behind the cue ball, pull backward, and release.
- A short click/tap only adjusts or preserves the aim and does not trigger an accidental shot.

## Running Locally

Simply open `index.html` in your browser.

To avoid restrictions in some browsers, you can also run a local server:

```bash
python3 -m http.server 8080
```

Then open:

```text
http://localhost:8080
```

## Deploying to GitHub Pages

1. Create a GitHub repository, for example `vigu-sinuca-arena`.
2. Upload the project files to the `main` branch.
3. In the repository, open **Settings → Pages**.
4. Under **Build and deployment**, select **Deploy from a branch**.
5. Select the `main` branch and the `/ (root)` folder.
6. Click **Save**.
7. After a few moments, GitHub will display the public URL for the game.

## Rules

The game follows a simplified version of 8-ball rules, designed for quick matches against the CPU:

- The first valid ball pocketed determines solids or stripes.
- After clearing your group, you must pocket the 8-ball.
- Pocketing the 8-ball too early results in a loss.
- Pocketing the cue ball is a foul, and the cue ball is automatically repositioned.

## Project Structure

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

You may use, modify, and publish this project on your GitHub account.

## V5 — Physics Adjustment

- Shots at 100% power now preserve significantly more energy over long distances.
- Rolling friction was recalibrated so the cue ball does not lose all of its energy before crossing the table.
- The stopping threshold uses visually compensated speed based on the table aspect ratio, keeping movement consistent at any angle.
- Maximum power received a small boost without changing the pull-and-release gesture.

## V6 — Mobile Landscape Mode

Mobile gameplay was optimized for landscape orientation:

- When starting a difficulty level on a touch device, the game attempts to enter fullscreen mode and request `landscape` orientation.
- On browsers that support `screen.orientation.lock("landscape")`, rotation occurs after the touch that starts the match.
- If the browser does not allow automatic orientation locking, the game displays a screen asking the player to rotate the device; once the phone is turned sideways, the match is automatically released.
- During landscape gameplay, the top bar is hidden and the HUD, table, and controls are compacted to use almost the entire viewport.
- The `manifest.webmanifest` defines `orientation: landscape` for use when the game is installed as a web app/PWA.

> **Note:** Mobile browsers do not allow a regular webpage to force screen rotation on page load without user interaction. Because of this, V6 uses fullscreen + the Screen Orientation API when available, with a visual fallback when it is not.

## V7 — Touch Pull-Back Fix

- The aim no longer rotates when the player touches the cue to pull it back.
- Touching the area behind the cue ball, where the cue is rendered, preserves the current aiming direction.
- During the pull-back gesture, the angle remains completely locked.
- Unintentional sideways finger movement is ignored when calculating shot direction.
- Touching another area of the table still allows the player to select a new direction.
- Desktop/mouse behavior remains unchanged.

## V8 — Correct Turns and Compact Mobile Support

### Turns

- If the player pockets a valid ball without committing a foul, they continue playing.
- The CPU only receives the turn when the player fails to pocket a valid ball or commits a foul.
- The same rule applies to the CPU.
- It is possible to pocket every ball in sequence without the opponent playing, as long as no shot is missed.
- First-contact validation now uses the state of the table at the beginning of the shot, preventing false fouls immediately after solids/stripes are assigned.
- Pocketing the final ball of your group and the 8-ball in the same shot does not count as a valid finish; the player must already be shooting for the 8-ball before the shot begins.

### Compact Mobile

- The HUD is forced into a single row during horizontal gameplay.
- Fixed the conflict with the 640px breakpoint that increased HUD height.
- Added layouts for screens around 568×320 and 640×360.
- Side controls are narrower and more compact.
- Improved support for safe areas and the available viewport.

## V9 FINAL — Universal Responsiveness and Faster Gameplay

### Responsiveness

- The power panel no longer depends on device-specific breakpoints.
- In mobile landscape mode, **"SHOT POWER"** automatically becomes **"POWER"**.
- The power meter uses the remaining vertical space instead of a fixed height.
- The layout uses `VisualViewport` to respect the space actually available when browser or Android navigation bars remain visible.
- On extremely narrow panels, buttons preserve their icons and hide text before the layout can overflow.
- The canvas uses a reduced DPR on touch devices to improve performance on lower-end phones.

### Match Pace

- Friction is now dynamic: powerful shots preserve range, while very slow final movement stops quickly.
- The next turn is released as soon as movement is no longer visually noticeable.
- CPU visual decision time was reduced.
- Physics simulation was reduced from 180 Hz to 120 Hz, preserving collision stability while lowering CPU usage on mobile.

## V10 FINAL — Power and Rack Break Improvements

- Cue power now uses a progressive curve: 50% remains controllable, while 80–100% becomes significantly stronger.
- A 100% shot increased from approximately 1.80 to 2.85 visual units of initial speed.
- Balls preserve more energy at high speed.
- Collision restitution was increased to transfer impact more effectively between balls.
- Cushions return slightly more speed.
- Very fast shots use adaptive physics substeps to reduce the risk of balls passing through each other during the break.
- Low-speed movement still decelerates quickly to avoid reintroducing delays between turns.

## V11 — Continuous Mobile Aiming

- Mobile aiming now behaves more like desktop mouse aiming.
- Touch and hold anywhere outside the cue pull zone, then move your finger to rotate the cue and aiming line continuously.
- Releasing the aiming gesture never shoots the cue ball.
- Shot charging remains a separate gesture: touch the cue behind the cue ball, pull backward, and release.
- Once charging starts, the aiming angle is completely locked.
- Sideways finger movement while charging does not alter the aim.
- Desktop controls, physics, CPU behavior, rules, sound, power curve, responsive landscape mode, and GitHub Pages deployment remain unchanged.
