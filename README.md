# Coordinator

A zero-dependency, single-file HTML5 educational game designed to teach Cartesian coordinates to children. The game uses procedural generation, interactive canvas rendering, and the native Web Audio API to create a fun, retro-arcade learning experience without needing a complex build pipeline or external assets.

## 🚀 Features

*   **Dynamic Grid System:** Configurable grid scales (±5, ±10, ±20, ±50, ±100) with auto-adjusting step intervals to keep the UI readable.
*   **Procedural Path Generation:** A randomized engine that generates non-repeating target sequences to ensure infinite replayability.
*   **Interactive Coordinate Feedback:** Real-time, responsive hover tooltips that map pointer coordinates to the grid. Features smart edge-detection to prevent tooltips from clipping off-screen.
*   **Quadrant Learning System:** A toggleable hint feature that visually highlights and labels the correct mathematical quadrant (I, II, III, IV) of the active target.
*   **Native Web Audio:** All sound effects (zaps, success chimes, error buzzes, and win jingles) are procedurally generated using the browser's `AudioContext` API. No external `.mp3` or `.wav` files required.
*   **Canvas-Based Rendering:** All visual assets, including the retro Pac-Man style ghost bots, gridlines, and animations, are drawn purely with the HTML5 `<canvas>` API.

## 🛠️ Technical Stack

*   **Core:** HTML5, CSS3, Vanilla JavaScript (ES6+)
*   **Styling:** Tailwind CSS (via CDN)
*   **Typography:** Google Fonts (`VT323` and `system-ui`)
*   **APIs Used:**
    *   `CanvasRenderingContext2D` (Graphics)
    *   `AudioContext` (Procedural Sound Generation)
    *   `requestAnimationFrame` (Game Loop / Animations)

## 🎮 How to Run

Because this project has zero local dependencies, running it is entirely plug-and-play:

1. Download or copy the `index.html` file.
2. Open the file directly in any modern web browser (Chrome, Firefox, Safari, Edge).
3. *Note: Sound effects require an initial user interaction (like clicking) to unlock the browser's AudioContext.*

## 🧠 Core Logic Overview

### Coordinate Mapping
The core of the engine relies on translating underlying mathematical coordinates (Grid Space) to visual pixels (Screen Space). The grid handles inverted Y-axes (since canvas Y grows downwards, but mathematical Y grows upwards) via utility functions:
*   `getPixelX(gridX)` / `getPixelY(gridY)`: Translates math to screen.
*   `getRawGridX(pixelX)` / `getRawGridY(pixelY)`: Translates screen to math.
*   `snapToGrid(rawVal)`: Snaps pointer input to the nearest valid intersection based on the current `gridStep`.

### Render Loop
The game utilizes a `requestAnimationFrame` loop (`gameLoop()`). Instead of re-rendering every single frame, it primarily redraws when an interaction occurs or when temporal effects (like the knockout animations) are active. 

### Path Engine
The `generateRandomPath()` function builds the level sequence. It queries the current grid bounds and step size, calculates valid coordinates, and ensures consecutive points are not identical, generating a fresh path every time "Next Level" is clicked.
