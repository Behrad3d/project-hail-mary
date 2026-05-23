# Astrophage Visualizer — Project Hail Mary

> Companion code for the TechyWanders video on Project Hail Mary by Andy Weir.

📺 **Video:** `[URL TO BE ADDED]`

---

## What This Is

Andy Weir doesn't just write science fiction. He runs the numbers first, then writes the story.

*Project Hail Mary* is built around a fictional organism called **astrophage** — a photosynthetic microbe that feeds on CO₂, uses stellar radiation as its energy source, and reproduces through binary fission. It originated on Venus, migrated to the Sun along what the book calls the **Petrova line**, and began dimming solar output at a geometric rate. The math in the book is real enough to model.

This repo contains five iterative HTML visualizations built during the video — each one a step closer to accurately representing the astrophage life cycle as Weir described it. No frameworks. No build tools. No dependencies. Just a canvas, some math, and too many hours thinking about fictional microbes.

The code was written at various hours of the night. Comments are sparse. It's a whole thing.

---

## The Files

### `00_Astrophage.html` — Cellular Automaton
The first pass. A grid-based simulation of astrophage spreading across a stellar surface patch. Each cell tracks energy level and colony density. Three interactive sliders let you tune the organism's behavior in real time:

- **Reproduction rate** — how fast the colony doubles
- **Consumption rate** — how fast each cell drains stellar energy
- **Energy bias** — how strongly astrophage migrates toward brighter cells (0 = random walk, 1 = always seeks light)

The "solar output" meter is your civilization's countdown. Crank reproduction rate to max and watch it drop in seconds. This is the version that maps directly to the Jupyter notebook in the video.

**Key concept introduced:** Cellular automaton, agent-based migration, geometric growth.

---

### `01_Astrophage.html` — Solar System Traversal Map
A top-down solar system view with four phases you step through manually. Planets are static. The focus here is on the **story arc** — where astrophage came from, where they went, and what happened when they got there.

Phases: Origin → Migration → Infection → Crisis

The Petrova line appears as a faint dashed guide between Venus and Sol. Solar output and Venus CO₂ update per phase. The Sun visibly darkens in phases 3 and 4.

**Key concept introduced:** The Petrova line. The four-phase narrative. Infection spots on the solar surface.

---

### `02_Astrophage.html` — Life Cycle Map (Five Phases)
The book is specific: astrophage don't just migrate to the Sun and stay there. They cycle. They energize at Sol, travel to Venus at 0.92c, collect CO₂, reproduce through mitosis, and return to Sol — both parent and child. Every round trip, the colony doubles.

This version adds the **correct life cycle** with five manually-navigated phases:

1. **Energize** — orbit Sol, absorb radiation
2. **Migrate out** — stream toward Venus along the Petrova line
3. **Breed on Venus** — collect CO₂, mitosis at the midpoint, `× 2` label appears
4. **Return × 2** — doubled colony streams back, two particle colors (amber = originals, orange = children)
5. **Crisis** — 14 cycles in, Sun dark, Venus CO₂ depleted

The Petrova line gets thicker and brighter with each cycle. Animated dashes show traffic direction.

**Key concept introduced:** Round-trip life cycle. Colony doubling. Bidirectional Petrova line traffic.

---

### `03_Astrophage.html` — Continuous Timeline
Removes the manual phase tabs. The animation plays automatically, advances through all 8 cycles, and runs to crisis on its own. A timeline bar at the bottom tracks progress and turns from green to red as solar output drops.

Controls: play / pause / reset / speed (1×, 2×, 4×).

Stats update live: solar output %, Venus CO₂ %, colony size (doubling each inbound phase), and year. The description text updates per stage so you can read what's happening while it plays.

**Key concept introduced:** Continuous playback. Real-time stat evolution. Colony counter updating mid-inbound.

---

### `04_Astrophage.html` — Orbital Motion (Final Version)
The complete version. Everything from `03` plus:

- All four planets orbit the Sun at **correct relative speeds** (Mercury = 0.24yr, Venus = 0.615yr, Earth = 1yr, Mars = 1.87yr scaled to fit the animation)
- Each planet leaves a **fading orbital trail** showing recent position history
- The **Petrova line rotates with Venus** — it's no longer a fixed horizontal line, it tracks wherever Venus currently is in its orbit
- Astrophage particles follow the current Sun→Venus vector, so the migration stream changes direction as Venus moves
- Planet labels push outward from the Sun center so they don't overlap the body

This is the version shown on screen in the video.

**Key concept introduced:** Dynamic orbital positions. Petrova line as a rotating vector. Perpendicular spread along an arbitrary path direction.

---

## The Science (Weir's Model)

Astrophage behavior as defined in *Project Hail Mary*:

| Property | Detail |
|---|---|
| Feed vector | CO₂ — collected from Venus upper atmosphere (50km altitude, 90 atm near-pure CO₂) |
| Energy source | Stellar radiation — photosynthetic |
| Migration speed | 0.92c along the Petrova line |
| Navigation | CO₂ spectral lines at 4.26μm and 18.31μm |
| Reproduction | Binary fission — one cell becomes two |
| Cycle | Sol (energize) → Venus (breed) → Sol (both return) |
| Growth rate | Geometric — colony doubles each complete cycle |
| Solar impact | ~10% output reduction over 30 years |

The Petrova line is named after Irina Petrova, the scientist who first identified the infrared trail between Venus and the Sun produced by astrophage propulsion.

---

## How to Run

No setup required. Open any file directly in a browser:

```bash
# Option 1: just double-click the file in Finder / Explorer

# Option 2: quick local server if you prefer
python3 -m http.server 8000
# then open http://localhost:8000/04_Astrophage.html
```

Tested in Chrome, Firefox, and Safari. Requires a browser with Canvas 2D API support (anything from the last 5 years is fine).

---

## Tech Stack

| What | How |
|---|---|
| Rendering | HTML5 Canvas 2D API |
| Animation | `requestAnimationFrame` loop |
| Particle system | Deterministic — positions computed from tick + seeded pseudo-random offsets, no simulation state |
| Orbital mechanics | Kepler approximation — constant angular velocity per planet, scaled to fit animation duration |
| Dependencies | None |
| Build tools | None |
| Framework | None |

The seeded random function (`sr()`) uses a sine-based hash so particle positions are stable and reproducible from a single integer seed — no stored state, no flickering.

---

## Repo Structure

```
/
├── 00_Astrophage.html   # Cellular automaton, interactive sliders
├── 01_Astrophage.html   # Solar system map, 4 manual phases
├── 02_Astrophage.html   # Life cycle map, 5 manual phases + Petrova line
├── 03_Astrophage.html   # Continuous timeline, play/pause/speed
├── 04_Astrophage.html   # Final — orbital planet motion
├── astrophage.css       # Shared styles across all visualizations
└── README.md            # This file
```

---

## Related

- 📺 Video: `[URL TO BE ADDED]`
- 📚 *Project Hail Mary* — Andy Weir (2021)
- 🔭 TechyWanders: `[channel URL TO BE ADDED]`

---

*Code is provided as-is. It was written at midnight. The comments reflect that.*
