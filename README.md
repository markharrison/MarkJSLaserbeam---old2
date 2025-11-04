# MarkJSLaserbeam

🚀 A lightweight JavaScript library for creating laser beam effects on HTML5 Canvas, designed for web games and interactive applications.

[![npm version](https://img.shields.io/npm/v/@markharrison/markjslaserbeam)](https://www.npmjs.com/package/@markharrison/markjslaserbeam) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

MarkJSLaserbeam is a lightweight JavaScript library for rendering laser beam effects in web games and interactive applications. Built for performance and easy integration with HTML5 Canvas.

## Key Features

• Fast, dependency-free ES Module
• Realistic laser beam rendering with customizable color, width, and glow
• Designed for game loops and interactive effects
• Performance optimized for real-time animation
• Works in all modern browsers with Canvas support

## Installation

```bash
npm install @markharrison/markjslaserbeam --save
```

Or include `markjslaserbeam.js` directly in your HTML.

## Quick Start

```js
import { MarkJSLaserbeam } from "@markharrison/markjslaserbeam";

const canvas = document.getElementById("myCanvas");
const laser = new MarkJSLaserbeam(canvas);

// Add laser on click
canvas.addEventListener("click", (e) => {
  const rect = canvas.getBoundingClientRect();
  const x = e.clientX - rect.left;
  const y = e.clientY - rect.top;
  laser.fire({
    x1: 100,
    y1: 100,
    x2: x,
    y2: y,
    color: "#FF0000",
    width: 8,
  });
});

// Game loop
function gameLoop(deltaTime) {
  laser.update(deltaTime);
  laser.render();
  requestAnimationFrame(gameLoop);
}
requestAnimationFrame(gameLoop);
```

## Documentation

See [laserbeammark.md](./markjslaserbeam.md) for detailed developer documentation, API reference, and advanced usage.

## Test Application

Open `index.html` in your browser to explore and test laser beam effects and customization options.

## License

MIT License - see [LICENSE](./LICENSE) for details.
