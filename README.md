# Block Racer 3D

Block Racer 3D is a large, browser-based 3D driving and flight sandbox built with [Three.js](https://threejs.org/) and plain HTML/CSS/JavaScript. The game combines timed circuit racing, an open procedural world, military missions, vehicle combat, weather, and extensive vehicle customization in a single HTML file.

The main implementation is `v8.html`.

## Features

- Grand Prix racing across five tracks with three laps and CPU opponents
- Free-play mode with a procedurally generated, chunk-based open world
- War mode with missions, difficulty levels, objectives, vehicles, and medals
- Land, sea, air, and submarine vehicles
- Cars, buses, trucks, motorcycles, tanks, hovercraft, trains, boats, aircraft, and military vehicles
- Vehicle customization for paint, livery, finish, wheels, lights, exhaust, and effects
- Dynamic time of day, weather, clouds, fog, rain, snow, and storms
- Forest, desert, wetlands, mountains, jungle, volcanic, city, snow, ocean, and many other biomes
- NPC traffic and pedestrians, landmarks, roads, rivers, rails, airports, ports, and fuel locations
- Flying, VTOL, submarine, helicopter, train, on-foot, tanker, and special vehicle mechanics
- Chase, far, bumper, and cinematic cameras
- Minimap, world map, flight instruments, compass, HUD, split-screen support, and touch controls
- Optional controller/gamepad support
- Optional Firebase leaderboard and anonymous authentication
- Local settings and vehicle customization persistence through `localStorage`

## Getting Started

Because `v8.html` is a JavaScript module and loads browser dependencies over HTTPS, serve it through a local web server instead of opening it directly with `file://`.

### Using VS Code

1. Open this folder in VS Code.
2. Install or use the Live Server extension.
3. Open `v8.html`.
4. Start Live Server and use the address it provides.

### Using Python

From this folder:

```powershell
python -m http.server 8080
```

Then open:

```text
http://localhost:8080/v8.html
```

### Using Node.js

From this folder:

```powershell
npx serve .
```

Then open the local URL printed by `serve`.

## Game Modes

### Grand Prix

Choose a stage, vehicle, and whether CPU rivals are enabled. Each race consists of three laps. Finish at the result screen to enter a racer name and submit a local or Firebase-backed leaderboard record.

The included stages are:

1. Beginner Oval Circuit
2. Over-Under Figure 8
3. The ZigZag Chicanes
4. Mountain Hairpins
5. Apex Pro Championship

### Free Play

Explore a continuously generated open world, change vehicles, discover landmarks, enter NPC traffic, or use trains, aircraft, ships, and on-foot travel. The world supports multiple biomes and environmental surface effects.

Free-play options include NPC density, minimap display, biome selection, world cohesion, surface handling, level of detail, and a performance/balanced/graphics rendering mode.

### War Mode

Select a mission, vehicle, and difficulty to enter combat operations in the free-play world. Mission objectives can include enemies, escorts, recon, captures, destruction, and survival-style tasks. Mission completion produces a debrief, medal, and statistics.

## Basic Controls

Controls may change with the active vehicle. The game pauses and displays vehicle-specific hints while you play.

| Action | Keyboard |
| --- | --- |
| Accelerate / climb / throttle | `W` |
| Brake / reverse / descend / throttle down | `S` |
| Steer / turn / bank | `A` / `D` |
| Handbrake | `Space` |
| Pitch / forward and back | Arrow keys, or vehicle-specific pitch controls |
| Change camera | `C` |
| Change vehicle in free play | `V` |
| Open world map | `M` |
| Pause / settings | `Esc` |
| Get in or out of a vehicle | `F` |
| Landing gear | `G` |
| Attack mode | `T` |
| Fire missile or main weapon | `F` or `Enter` |
| Cannon / gun | Hold `E` |
| Torpedo | `Q` |
| Catapult / tailhook | `L` / `H` |
| Supersonic | `N` |
| VTOL / special aircraft mode | `B` |
| Eject | `Y` |
| Job board | `K` |
| Photo mode | `O` |
| Record / play replay | `R` / `P` |
| Split screen | `F2` |

Additional controls are shown in the pause menu and in the hint card for the selected vehicle.

### Aircraft and Helicopters

- Fixed-wing aircraft use `W` / `S` for throttle and arrow keys or `Space` / `Shift` for pitch, depending on the aircraft.
- Helicopters use `W` / `S` to climb or descend and arrow keys to move forward or backward.
- `A` / `D` handles turning or banking.
- Some aircraft support gear, VTOL, supersonic, tailhooks, catapults, bombing, flares, and refueling.

### Water, Land, and Special Vehicles

- Cars and bikes use `W` / `S` for acceleration and braking and `A` / `D` for steering.
- Boats and ships use throttle and rudder controls.
- Submarines use `Space` and `Shift` to dive or surface.
- Tanks support turret aiming, guns, and missile or machine-gun attacks.
- Trains use `W` for power and `S` for braking.

### Touch Controls

Touch buttons appear automatically on supported touch layouts. The game includes left, right, accelerate, brake, climb, and descend controls, while the vehicle-specific hint card documents other available actions.

### Gamepads

A standard browser gamepad is supported. It combines with keyboard input instead of replacing it. Axis 0 steers, axis 1 provides throttle, and common face and trigger buttons provide acceleration, braking, and other vehicle actions.

## Settings

The gear icon opens quick settings for:

- Camera mode
- Time of day
- Weather
- Cloud density
- NPCs and NPC density
- Mini map
- Biome mode
- World cohesion
- Surface handling
- Level of detail
- Render quality
- Debug overlays

Settings and some customization state are saved in `localStorage` under `gem8_settings`. Most settings can also be changed in the pause menu.

## Firebase Leaderboard

The leaderboard is optional. The file reads Firebase configuration from injected globals when available:

- `__firebase_config`
- `__initial_auth_token`
- `__app_id`

If those globals are absent or contain no valid API key, the game falls back to a mock configuration and disables the global leaderboard with a console warning. Local leaderboard behavior may still be available in the user interface depending on the runtime.

To enable Firebase:

1. Create a Firebase project.
2. Enable Firestore and Anonymous Authentication.
3. Provide valid Firebase configuration and app globals when serving or embedding the HTML.
4. Add Firestore rules appropriate for the authenticated users and records your deployment supports.

Do not expose private service credentials in a browser game. Only browser-safe Firebase client configuration should be included in the page.

## Dependencies

The HTML loads these libraries directly from CDNs:

- Three.js `0.128.0`
- Firebase JavaScript SDK `11.6.1`

An internet connection is required unless these dependencies are vendored and the import URLs are changed locally.

## Project Files

- `v8.html` - Main current game implementation
- `v8perf.html` - Performance-oriented variant
- `v8.backup.html` - Backup of the main implementation
- `legacy/` - Earlier development versions

## Development Notes

- The main application is a single module inside `v8.html`.
- Rendering uses Three.js scenes, meshes, shared geometry/material caching, and dynamic chunk unloading.
- The open world is divided into 400-unit chunks with a configurable loading radius.
- World objects are generated procedurally and themed by biome and weather.
- Vehicle logic is implemented per vehicle category and vehicle type.
- Rendering quality can be reduced through the in-game performance modes and LOD settings.
- Browser console logging provides leaderboard, replay, and debug diagnostics.

## Troubleshooting

### The page is blank or imports fail

- Make sure the file is served over HTTP or HTTPS.
- Check the browser console for CDN or module loading errors.
- Confirm that the browser has internet access.
- Try a current desktop browser with WebGL enabled.

### The game is slow

- Open the video settings and choose `PERFORMANCE`.
- Lower LOD and cloud settings.
- Reduce NPC density.
- Disable minimap/debug overlays.
- Close other GPU-intensive browser tabs.

### Leaderboard records do not submit

- Check whether Firebase configuration and authentication are available.
- Confirm that anonymous authentication is enabled.
- Check Firestore rules and browser console errors.
- Firebase configuration is optional; the game can still run without it.

### Controls are sticky or not responding

- Release the affected key or touch control and refocus the browser window.
- Press `Esc` to open or close the pause menu.
- If a gamepad is connected, unplugging or reconnecting it may reset browser input state.
