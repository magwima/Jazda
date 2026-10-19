# Jazda! Polish Streets

A street-skating racer through Warsaw, Rzeszów, Gdańsk and Wrocław. Play it in real 3D (the default), in smooth 2.5D HD, or in the original pixel-art style. It is one HTML file: no build step, no server, no paid libraries. The 3D view loads the free Three.js library from a CDN when it's used. All the art and music is generated in code.

## Play it on GitHub Pages

1. Create a new repository (for example `jazda`) and upload `index.html`, `README.md` and `.nojekyll`.
2. Go to **Settings → Pages**. Under **Source**, choose **Deploy from a branch**, then pick **main** and **/(root)**, and click **Save**.
3. After a minute or two the game is live at `https://<your-username>.github.io/jazda/`.

To play it on your own computer, open `index.html` in Chrome, Edge, Firefox or Safari. Optional asset files only load when the game is served over HTTP (GitHub Pages, or `python3 -m http.server` in this folder).

## Controls

| Action | Keyboard (remappable in Options) | Touch |
| --- | --- | --- |
| Change lane | ← → or A D | Swipe left or right |
| Jump (ollie) | Space, ↑ or W | Swipe up |
| Manual (on the ground) | ↓ or S, hold | Swipe down and hold |
| Flip trick (in the air) | K; add ← → ↑ ↓ for other flips | Tap |
| Grab trick (in the air) | L, hold, and release before landing | GRAB button |
| Boost | Shift | BOOST button |
| Shoot paint | F | Tap, or the FIRE button |
| Balance on a rail | ← → | Swipe left or right |
| Pause | Esc or P | II button |

## Features

- **Two modes:** Race (you against 3 AI rivals, about 2 minutes) and Score Run (90 seconds).
- **Four cities**, each with its own landmarks, colours, music and a day/night cycle. Weather can be clear, rain or snow.
- **Three difficulties** (Easy, Hard, Expert). They change top speed, obstacle density, rival skill and aggression, the rail catch window, balance drift and the score multiplier.
- **Moves:** grinds with a balance meter, flip and grab tricks, manuals, combos, a boost meter, kicker ramps and boost pads.
- **Paint shot:** unlock it in the skill tree or pick up paint crates. Rivals on Hard and Expert shoot back, but always flash a red "!" first.
- **Progression:** XP levels, stars, skill points, a 5 × 3 skill tree, 5 boards, outfits, decals, trails and victory poses.
- **Collectibles:** 20 hidden items, 5 per city (mermaid badges, golden pączki, seagulls and gnomes).
- **Saving:** auto-saves to `localStorage` with a versioned format, plus JSON export and import.
- **Accessibility:** colourblind mode (shapes and outlines, not only colour), three text sizes, reduced motion, subtitles for every voice line, remappable keys and full keyboard menus.
- **3D view (default):** a chase camera behind your skater on real curved, hilly streets built from the same track: buildings with detailed facades, trees, lamps, bridges with steel arches, harbour water and cranes, trams, kiosks and obstacles in 3D, cartoon skaters with animated tricks, shadows, bloom, day/night, rain and snow, and a gently rolling world. If 3D can't start (no WebGL or no connection), the game uses the HD view.
- **Graphics style:** HD draws the world at full screen resolution. The skaters, buildings, trees and billboards are redrawn as detailed smooth art (shaded clothes, faces, hair, window frames, cornices, balconies, brickwork, lit rooms at night); other sprites are smoothly upscaled. It also adds soft shadows, layered clouds, street-lamp light pools, wet-road reflections, bloom and detailed asphalt. Pixel switches back to the original 400 × 225 look. Change it in Options → Graphics → Style (3D, HD or Pixel).
- **Performance:** Auto quality drops to Medium or Low when the frame rate falls, then steps back up.

## Optional assets

Every asset is optional. To replace generated art or music, add an `assets` folder and an `assets/manifest.json`, for example:

```json
{
  "chars": { "stary": { "back": "chars/stary_back.png", "front": "chars/stary_front.png" } },
  "music": { "warsaw": ["music/warsaw.ogg", "music/warsaw.mp3"] },
  "vo": { "stary": { "go": "vo/stary_go.ogg" } },
  "bg": { "gdansk": { "far": "bg/gdansk_far.png" } }
}
```

- **Back-view sheets** (`<id>_back.png`): 384 × 512 px, frames of 48 × 64, 8 columns × 8 rows. The rows are ride, push, crouch, air, flip, grab, grind and bail.
- **Front sheets** (`<id>_front.png`): 576 × 256 px, frames of 96 × 128. The rows are idle and victory.
- **Music:** a seamless loop of 60–180 s, in OGG plus MP3.
- **Voice lines:** short mono clips named `go`, `trick`, `crash`, `hit`, `win` and `lose`.
- **Backgrounds** (`<city>_sky.png`, `_far.png`, `_near.png`): 800 × 225 px.

Character ids are `stary`, `stara`, `kuba` and `ola`. City ids are `warsaw`, `rzeszow`, `gdansk` and `wroclaw`. The full asset list, with naming rules, is in the design pack.

## Code layout (inside `index.html`)

| Module | What it does |
| --- | --- |
| CORE | Constants, maths, seeded RNG, game data (difficulties, cities, characters, boards, cosmetics, skills, tricks) |
| SAVE / INPUT | Versioned save with migration, export and import; remappable keyboard, touch swipes and buttons |
| ART | Pixel font, palettes, characters (back and front views), props, buildings, skylines |
| TRACK | Seeded road layout, city zones, scenery, obstacle patterns with a guaranteed free path, rails, pickups |
| SKATER | Shared physics for the player and the AI: lanes, jumps, flips, grabs, manuals, grinds, boost, crashes |
| GAME | Race flow, rival AI, collisions, pickups, paint pellets, positions, rewards |
| RENDER 3D | Optional Three.js renderer: track-to-world path, streets, buildings, props, skater models and poses, streaming, particles, weather, bloom |
| RENDER | Pseudo-3D road, parallax, sprites with hill clipping, lights, particles, weather, motion blur, colour split, vignette; HD mode (Scale2x sprite upscaling, bloom, lamp lighting) |
| AUDIO | Web Audio music sequencer per city, synthesized sound effects, rolling and grind loops, voice lines |
| UI / MAIN | Menus, HUD, pause and results screens; game loop and adaptive quality |

## Roadmap

- **Next:** Kraków and Poznań, a daily seeded challenge, a ghost of your best run.
- **Then:** online leaderboards, ghost races with friends, track share codes, live races for 2 to 4 players (these need a small backend).
- **Later:** seasonal events (Christmas markets, Juwenalia, a Baltic summer), a track editor.

## Credits

Game design and direction by Dasz. Code, pixel art and music were generated by Claude. Fonts: Pixelify Sans and Barlow Semi Condensed (SIL Open Font License). Every shop and brand in the game is invented.
