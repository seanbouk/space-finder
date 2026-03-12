# Space Finder

A hill-climbing algorithm that searches for dense, walkable, human-scale layouts on a grid — the kind of pattern you might find in a cottage court or medieval village.

**[Try it live](https://seanbouk.github.io/space-finder/)**

## How it works

A 20x20 grid starts all white (open space). Each tick, the algorithm toggles a random cell and keeps the change if the overall score improves. When a single toggle fails, it tries a compound 2-cell move — toggling a neighbour as well — which lets it break through corridors and reshape paths.

Hard rules are scored as countable violations rather than binary pass/fail, so the algorithm can gradually fix a broken grid (e.g. after hitting Noise to randomise).

### Hard rules

- **Access** — every house (black) has at least one walkable (white) neighbour
- **Connectivity** — all walkable space forms one connected region
- **No diagonal touch** — two houses can't touch only at a corner

### Soft rules (scored, weights adjustable)

- **Density** — pack in as many houses as possible
- **Vista** — penalise long straight corridors in all four directions including diagonals (cubic penalty for runs > 3)
- **Enclosure** — reward bends and corners in paths
- **Plaza** — penalise wide open 2x2 white blocks
- **Dead-end** — penalise white cells with only one way out
- **T-junction** — reward three-way intersections with proper corner framing
- **Bulk** — penalise large contiguous house masses (bounding box area > 50)

## Usage

Open `index.html` in a browser, hit Start, and watch it go. Click and drag on the grid to draw — mousedown toggles a cell and sets the paint colour, then drag to keep painting. The simulation pauses while drawing and resumes on release. Hit Noise to randomise the grid and let the algorithm resolve it. Adjust the weight sliders to steer toward different layouts. Slider positions persist in localStorage.
