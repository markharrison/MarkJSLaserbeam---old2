# MarkJSLaserbeam Class Documentation

A configurable laser beam effect system with multiple visual styles, particle effects, smooth animations, and support for multiple simultaneous laser beams.

## Basic Usage

```javascript
import { MarkJSLaserbeam } from './lib/markjslaserbeam.js';

// Create a laser system (instantiate once)
const laserSystem = new MarkJSLaserbeam(canvas, {
    beamStyle: 'solid',
    coords1: [50, 100],
    coords2: [400, 100],
    beamColor: '#00ffff',
    glowColor: '#00ffff',
    tipColor: '#ffffff',
    tipSize: 20,
});

// In your game loop
laserSystem.update(deltaTime);
laserSystem.render();

// Fire multiple lasers with different positions and settings
laserSystem.addLaser(1, {
    coords1: [0, 100],
    coords2: [800, 100],
    beamColor: '#ff0000'
});

laserSystem.addLaser(1, {
    coords1: [0, 200], 
    coords2: [800, 200],
    beamColor: '#00ff00',
    beamStyle: 'plasma'
});

// Backwards compatibility - fire with default options
laserSystem.fire(1);  // Still works!
```

## Multi-Laser System

MarkJSLaserbeam now supports multiple simultaneous laser beams following the ParticlesMark pattern:

- **Single Instance**: Create one `MarkJSLaserbeam` instance per canvas
- **Multiple Lasers**: Use `addLaser()` to fire multiple beams with different positions and properties
- **Automatic Management**: The system handles all active lasers automatically
- **Memory Management**: Use `destroy()` to clean up all resources

### Key Methods

#### `addLaser(direction = 1, options = {})`

Adds a new laser beam with custom options. Returns a unique laser ID.

**Parameters:**
- `direction` (number):
  - `1` = fire from coords1 to coords2 (default)
  - `-1` = fire from coords2 to coords1 (reverse)
  - `0` = instant appear then fade (no shooting animation)
- `options` (object): Laser-specific configuration (overrides defaults)

```javascript
// Fire laser with custom position and color
const laserId = laserSystem.addLaser(1, {
    coords1: [100, 50],
    coords2: [700, 350],
    beamColor: '#ff4444',
    beamStyle: 'tazer'
});
```

#### `removeLaser(id)`

Removes a specific laser by ID. Returns `true` if laser was found and removed.

```javascript
laserSystem.removeLaser(laserId);
```

#### `getActiveLaserCount()`

Returns the number of currently active laser beams.

```javascript
const count = laserSystem.getActiveLaserCount();
console.log(`Active lasers: ${count}`);
```

#### `clearAllLasers()`

Immediately removes all active laser beams.

```javascript
laserSystem.clearAllLasers();
```

#### `destroy()`

Destroys the laser system and cleans up all resources. Call this when done with the laser system.

```javascript
laserSystem.destroy();
```

## Constructor Options

### Basic Properties

| Option          | Type     | Default                           | Description                                       |
| --------------- | -------- | --------------------------------- | ------------------------------------------------- |
| `coords1`       | `[x, y]` | `[0, canvas.height/2]`            | First coordinate point of the laser               |
| `coords2`       | `[x, y]` | `[canvas.width, canvas.height/2]` | Second coordinate point of the laser              |
| `shootDuration` | `number` | `800`                             | Time (ms) for beam to travel between coordinates  |
| `fadeDuration`  | `number` | `800`                             | Time (ms) for beam to fade out after reaching end |

### Visual Properties

| Option      | Type     | Default     | Description                                    |
| ----------- | -------- | ----------- | ---------------------------------------------- |
| `beamStyle` | `string` | `'solid'`   | Visual style (see Beam Styles below)           |
| `beamColor` | `string` | `'#00ffff'` | Primary color of the beam                      |
| `glowColor` | `string` | `'#00ffff'` | Color of the glow effect                       |
| `tipColor`  | `string` | `glowColor` | Color of the beam tip (defaults to glow color) |
| `beamWidth` | `number` | `4`         | Width of the beam in pixels                    |
| `glowSize`  | `number` | `24`        | Size of the glow effect                        |
| `tipSize`   | `number` | `24`        | Size of the beam tip                           |
| `tipStyle`  | `string` | `'arrow'`   | Tip style: `'arrow'` or `'circle'`             |

### Particle Configuration

| Option           | Type     | Default   | Description                   |
| ---------------- | -------- | --------- | ----------------------------- |
| `particleConfig` | `object` | See below | Particle system configuration |

#### Particle Config Properties

```javascript
particleConfig: {
    color: '#fff',           // Particle color
    glowColor: '#00ffff',    // Particle glow color
    size: 6,                 // Base particle size
    speed: 3,                // Particle movement speed
    life: 600,               // Particle lifetime (ms)
    fade: true,              // Whether particles fade out
    rate: 0.8                // Emission rate (0-1, higher = more particles)
}
```

## Beam Styles

### `'solid'`

Clean, straight laser beam - perfect for precise weapons.

### `'dashed'`

Dashed line effect - good for energy weapons with interrupted power.

### `'crackling'`

Electric crackling effect with small random deviations - ideal for electrical weapons.

### `'tazer'`

Sharp zigzag electrical bolts with dramatic turns - perfect for taser/electric shock effects.

### `'pulsing'`

Beam width pulses and throbs - great for charging or unstable energy weapons.

### `'charged'`

Multiple thin beams bundled together - excellent for high-tech energy rifles.

### `'plasma'`

Multi-layer glow effect with bright core - perfect for plasma cannons.

### `'disruptor'`

Fragmenting beam that splits and merges - ideal for experimental/alien weapons.

## Tip Styles

The laser beam tip can be configured using the `tipStyle` option:

### `'arrow'` (default)

Sharp diamond/arrow-shaped tip that points in the direction of beam travel. Provides clear directional indication and sharp visual impact.

### `'circle'`

Simple circular tip that glows at the beam endpoint. More subtle than arrow tips and good for energy-based weapons where direction is less important.

## Public Methods

### `fire(direction = 1)` (Backwards Compatibility)

Fires a laser beam using default options. This method is maintained for backwards compatibility.

**Parameters:**
- `direction` (number): Same as `addLaser()` direction parameter

```javascript
laserSystem.fire(1); // Normal direction
laserSystem.fire(-1); // Reverse direction  
laserSystem.fire(0); // Instant appear
```

### `addLaser(direction = 1, options = {})`

Adds a new laser beam with custom options. This is the preferred method for the multi-laser system.

**Returns:** Unique laser ID (number)

```javascript
// Basic usage
const id = laserSystem.addLaser(1);

// With custom options
const id = laserSystem.addLaser(1, {
    coords1: [0, 200],
    coords2: [800, 200], 
    beamColor: '#ff0000',
    beamStyle: 'plasma'
});
```

### `update(deltaTime)`

Updates all active laser animations. Call this every frame in your game loop.

```javascript
// In your game loop
laserSystem.update(deltaTime);
```

### `render()`

Renders all active laser beams to the canvas. Call this after update() in your render loop.

```javascript
// In your render loop
laserSystem.render();
```

### `removeLaser(id)`

Removes a specific laser by its ID.

**Returns:** Boolean indicating success

```javascript
const success = laserSystem.removeLaser(laserId);
```

### `getActiveLaserCount()`

Returns the number of currently active laser beams.

**Returns:** Number of active lasers

```javascript
const count = laserSystem.getActiveLaserCount();
```

### `clearAllLasers()`

Immediately removes all active laser beams.

```javascript
laserSystem.clearAllLasers();
```

### `destroy()`

Destroys the laser system and cleans up all resources. Call when done with the system.

```javascript
laserSystem.destroy();
```

## Properties

### `lasers` (readonly)

Array of currently active laser objects.

### For individual lasers:

### `active` (readonly)

Boolean indicating if a specific laser is currently active (shooting or fading).

### `phase` (readonly)

Current animation phase: `'idle'`, `'shoot'`, or `'fade'`.

### `progress` (readonly)

Animation progress from 0 to 1 during the shoot phase.

### `opacity` (readonly)

Current opacity from 1 to 0 during the fade phase.

## Examples

### Multi-Laser System

```javascript
// Create the laser system once
const laserSystem = new MarkJSLaserbeam(canvas);

// Fire multiple lasers at different positions
laserSystem.addLaser(1, {
    coords1: [0, 100],
    coords2: [800, 100],
    beamColor: '#ff0000',
    beamStyle: 'solid'
});

laserSystem.addLaser(1, {
    coords1: [0, 200], 
    coords2: [800, 200],
    beamColor: '#00ff00',
    beamStyle: 'plasma'
});

laserSystem.addLaser(1, {
    coords1: [0, 300],
    coords2: [800, 300], 
    beamColor: '#0000ff',
    beamStyle: 'charged'
});

// All lasers animate simultaneously
function gameLoop() {
    laserSystem.update(deltaTime);
    laserSystem.render();
    requestAnimationFrame(gameLoop);
}
```

### Crossfire Pattern

```javascript
const laserSystem = new MarkJSLaserbeam(canvas);

// Diagonal from top-left to bottom-right
laserSystem.addLaser(1, {
    coords1: [50, 50],
    coords2: [750, 350],
    beamStyle: 'tazer',
    beamColor: '#ffffff'
});

// Diagonal from top-right to bottom-left (delayed)
setTimeout(() => {
    laserSystem.addLaser(1, {
        coords1: [750, 50],
        coords2: [50, 350],
        beamStyle: 'crackling',
        beamColor: '#ff88ff'
    });
}, 300);
```

### Rapid Fire Sequence

```javascript
const colors = ['#ff4444', '#44ff44', '#4444ff', '#ffff44', '#ff44ff'];
const styles = ['solid', 'plasma', 'charged', 'pulsing', 'disruptor'];

for (let i = 0; i < 5; i++) {
    setTimeout(() => {
        const y = 200 + (i - 2) * 30; // Spread vertically
        laserSystem.addLaser(1, {
            coords1: [50, y],
            coords2: [750, y],
            beamStyle: styles[i],
            beamColor: colors[i],
            shootDuration: 600,
            fadeDuration: 1000
        });
    }, i * 150);
}
```

### Basic Horizontal Laser (Legacy Style)

```javascript
const horizontalLaser = new MarkJSLaserbeam(canvas, {
    coords1: [0, 200],
    coords2: [canvas.width, 200],
    beamStyle: 'solid',
    beamColor: '#ff0000',
});

// Still works with backwards compatibility
horizontalLaser.fire(1);
```

### Tazer Effect

```javascript
const tazer = new MarkJSLaserbeam(canvas, {
    coords1: [100, 50],
    coords2: [300, 400],
    beamStyle: 'tazer',
    beamColor: '#ffffff',
    glowColor: '#8888ff',
    tipColor: '#ffff88', // Bright yellow tip
    beamWidth: 6,
    tipSize: 30,
    tipStyle: 'arrow', // Sharp directional tip
});
```

### Energy Orb Beam

```javascript
const energyOrb = new MarkJSLaserbeam(canvas, {
    coords1: [200, 200],
    coords2: [600, 200],
    beamStyle: 'plasma',
    beamColor: '#00ff88',
    glowColor: '#00ff88',
    tipColor: '#ffffff', // White-hot tip
    tipSize: 20,
    tipStyle: 'circle', // Circular energy tip
});
```

### Hot Laser Beam

```javascript
const hotLaser = new MarkJSLaserbeam(canvas, {
    coords1: [50, 100],
    coords2: [750, 100],
    beamStyle: 'solid',
    beamColor: '#ff4444',
    glowColor: '#ff8888',
    tipColor: '#ffff00', // Yellow-hot tip
    tipStyle: 'arrow',
});
```

### Plasma Cannon

```javascript
const plasmaCannon = new MarkJSLaserbeam(canvas, {
    coords1: [playerX, playerY],
    coords2: [targetX, targetY],
    beamStyle: 'plasma',
    beamColor: '#00ff88',
    glowColor: '#00ff88',
    beamWidth: 8,
    shootDuration: 300,
    fadeDuration: 1000,
});
```

### Bidirectional Laser

```javascript
const bidirectionalLaser = new MarkJSLaserbeam(canvas, {
    coords1: [100, 100],
    coords2: [500, 300],
    beamStyle: 'charged',
});

// Fire in different directions
bidirectionalLaser.fire(1); // coords1 to coords2
bidirectionalLaser.fire(-1); // coords2 to coords1
bidirectionalLaser.fire(0); // instant appear
```

### Custom Particles

```javascript
const customLaser = new MarkJSLaserbeam(canvas, {
    beamStyle: 'crackling',
    particleConfig: {
        color: '#ffff00',
        glowColor: '#ff8800',
        size: 8,
        speed: 5,
        life: 800,
        rate: 0.9,
    },
});
```

### Integration Example

```javascript
class GameScene {
    constructor() {
        // Create one laser system instance
        this.laserSystem = new MarkJSLaserbeam(this.canvas, {
            beamStyle: 'plasma',
            coords1: [50, 150],
            coords2: [750, 150],
        });
    }

    handleInput(key) {
        if (key === 'Space') {
            // Fire laser with random vertical position
            const y = 100 + Math.random() * 200;
            this.laserSystem.addLaser(1, {
                coords1: [50, y],
                coords2: [750, y],
                beamColor: this.getRandomColor()
            });
        }
        if (key === 'Enter') {
            // Crossfire pattern
            this.fireCrossfire();
        }
        if (key === 'Escape') {
            // Clear all lasers
            this.laserSystem.clearAllLasers();
        }
    }

    fireCrossfire() {
        // Multiple diagonal lasers
        this.laserSystem.addLaser(1, {
            coords1: [0, 0],
            coords2: [800, 400],
            beamStyle: 'tazer'
        });
        
        setTimeout(() => {
            this.laserSystem.addLaser(1, {
                coords1: [800, 0], 
                coords2: [0, 400],
                beamStyle: 'crackling'
            });
        }, 200);
    }

    update(deltaTime) {
        this.laserSystem.update(deltaTime);
    }

    render() {
        // Clear canvas, draw other objects...
        this.laserSystem.render();
        
        // Show laser count
        this.drawText(`Active Lasers: ${this.laserSystem.getActiveLaserCount()}`);
    }

    destroy() {
        // Clean up when scene ends
        this.laserSystem.destroy();
    }
}
```

## Performance Notes

-   The laser system automatically manages multiple active laser beams
-   Each laser manages its own particle system independently
-   Particles are cleaned up automatically when they expire
-   Lasers become inactive after the fade phase completes and are removed automatically
-   Use reasonable particle rates (0.1 - 1.0) for good performance
-   The system is designed to handle dozens of simultaneous lasers efficiently
-   Use `destroy()` to clean up all resources when done with the laser system

## Private Methods

The following methods are internal implementation details and should not be called directly:

-   `_drawCracklingBeam()`
-   `_drawTazerBeam()`
-   `_drawPulsingBeam()`
-   `_drawChargedBeam()`
-   `_drawPlasmaBeam()`
-   `_drawDisruptorBeam()`
-   `_emitParticles()`
-   `_updateParticles()`
-   `_renderParticles()`

## Tips

1. **Timing**: Adjust `shootDuration` and `fadeDuration` to match your game's pace
2. **Colors**: Use contrasting `beamColor` and `glowColor` for better visibility
3. **Styles**: Choose beam styles that match your game's theme
4. **Particles**: Lower particle rates for performance, higher for visual impact
5. **Positioning**: Update `startCoords` and `endCoords` dynamically for moving lasers
