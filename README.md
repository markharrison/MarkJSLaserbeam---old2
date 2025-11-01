# MarkJSLaserbeam

A powerful JavaScript class for creating stunning laser beam effects with multiple visual styles, particle systems, smooth animations, and support for multiple simultaneous laser beams. Perfect for games, interactive applications, and visual effects.

![MarkJSLaserbeam Multi-Laser Demo](demo.png)

## Features

✨ **8 Distinct Beam Styles**: Solid, Dashed, Crackling, Tazer, Pulsing, Charged, Plasma, and Disruptor  
🎨 **Customizable Colors**: Independent beam, glow, and tip colors  
⚡ **Dynamic Firing Modes**: Forward, reverse, and instant firing directions  
🔥 **Particle Effects**: Configurable particle systems with sparks and trails  
🎯 **Tip Styles**: Arrow and circle tip options  
📏 **Flexible Dimensions**: Adjustable beam width, glow size, and tip size  
⏱️ **Timing Controls**: Configurable shoot and fade durations  
🚀 **Multi-Laser Support**: Multiple simultaneous laser beams with different positions and properties  
🧹 **Memory Management**: Proper resource cleanup with `destroy()` method  
🖱️ **Interactive Demo**: Complete web-based test application with multi-laser demonstrations

## Quick Start

### Installation

Simply include the `markjslaserbeam.js` file in your project:

```javascript
import { MarkJSLaserbeam } from "./markjslaserbeam.js";
```

### Basic Usage

```javascript
// Create a laser system (instantiate once)
const laserSystem = new MarkJSLaserbeam(canvas, {
  beamStyle: "plasma",
  beamColor: "#00ffff",
  glowColor: "#00ffff",
});

// In your game loop
laserSystem.update(deltaTime);
laserSystem.render();

// Fire multiple lasers at different positions
laserSystem.addLaser(1, {
  coords1: [50, 100],
  coords2: [400, 150],
  beamColor: "#ff4444",
});

laserSystem.addLaser(1, {
  coords1: [50, 200],
  coords2: [400, 250],
  beamColor: "#44ff44",
  beamStyle: "charged",
});

// Backwards compatibility
laserSystem.fire(1); // Still works!
```

## Interactive Demo

The repository includes a comprehensive interactive demo application (`index.html`) that showcases all MarkJSLaserbeam features:

**To run the demo:**

1. Start an HTTP server: `python3 -m http.server 8000`
2. Open `http://localhost:8000` in your browser
3. Experiment with different beam styles, colors, and effects in real-time

The demo features:

- **Beam Style Selection**: Test all 8 beam effects
- **Real-time Controls**: Adjust colors, dimensions, timing, and particles
- **Fire Controls**: Test different firing modes and tip styles
- **Preset Demonstrations**: Quick-access buttons for common configurations
- **Multi-Laser Demos**: Showcase multiple simultaneous laser beams
  - **Multi-Layer Barrage**: Three lasers at different heights with staggered timing
  - **Crossfire Pattern**: Diagonal lasers from opposite corners
  - **Rapid Fire Sequence**: Sequential laser burst with different colors and styles
- **Active Laser Counter**: Real-time display of active laser count

## Documentation

For detailed developer documentation, API reference, and advanced usage examples, see:

📖 **[MarkJSLaserbeam Documentation](markjslaserbeam.md)**

The documentation covers:

- Complete API reference
- All beam styles with descriptions
- Configuration options
- Integration examples
- Performance tips

## Files

- `markjslaserbeam.js` - Main MarkJSLaserbeam class
- `markjslaserbeam.md` - Detailed developer documentation
- `index.html` - Interactive demo application
- `README.md` - This overview

## Browser Compatibility

MarkJSLaserbeam uses ES6 modules and requires a modern browser with Canvas 2D support. The demo must be served through an HTTP server due to ES6 module security requirements.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
