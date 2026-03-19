# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Sammy Pong is a browser-based Pong game — a single self-contained `index.html` file with embedded CSS and JavaScript. No build system, no dependencies, no tooling required.

To run: open `index.html` in any modern browser.

## Architecture

Everything lives in `index.html`:

- **HTML** (lines 1–62): Canvas element (700×480), score display, control instructions
- **CSS** (lines 7–52): Dark theme, gradient title, canvas styling
- **JavaScript** (lines 63–211): Full game engine

### Game Engine Structure

- **Constants**: Canvas dimensions, paddle size, ball size, speeds
- **State object**: Paddle positions/scores, ball position/velocity
- **Input**: `A`/`D` keys for Player 1 (bottom, orange); arrow keys for Player 2 (top, blue)
- **`update()`**: Paddle movement, ball physics, collision detection, scoring
- **`draw()`**: Renders background, center line, paddles (`roundRect`), ball
- **`loop()`**: `requestAnimationFrame` game loop calling update → draw each frame

### Scoring

- Player 1 scores when ball exits top boundary; Player 2 scores when ball exits bottom
- Score display format: `player2_score — player1_score`
- Ball resets to center with a random angle after each score

### Ball Physics

Bounce angle varies based on where the ball hits the paddle (±30° range), giving players directional control.
