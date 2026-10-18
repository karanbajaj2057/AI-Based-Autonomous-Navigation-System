# AutoNav.sim — AI Autonomous Navigation Simulator

An interactive browser-based robotics playground for exploring grid-based autonomous navigation. Select a scenario, edit the map, choose a search algorithm, plan a route, and step through the robot's simulated navigation loop.

**Live demo:** https://autonavsim.lovable.app  
**Repository:** `AutoNav-Sim`

> This repository is a standalone React implementation inspired by the publicly visible AutoNav.sim demo. It is not an export of Lovable's private source code. Review and replace screenshots, branding, and implementation details as needed before publishing it as your own project.

## Features

- **Interactive grid editor:** add walls, erase cells, and move start and goal positions.
- **Scenario presets:** Warehouse AMR, Urban blocks, Maze / search & rescue, and Agri field / rocks.
- **Path-planning algorithms:** A*, Dijkstra, Greedy Best-First Search, and Breadth-First Search.
- **Eight-direction movement:** orthogonal and diagonal steps with diagonal corner-cutting prevention.
- **Perception visualization:** simulated 360° LiDAR-style rays and a configurable sensor overlay.
- **Navigation controls:** plan a route, navigate, pause, resume, and reset a run.
- **Mission telemetry:** robot position, planned path cost, distance travelled, expanded nodes, planning time, and progress.
- **Event log:** readable status messages for route planning and navigation.
- **Responsive interface:** dark dashboard layout for desktop and smaller screens.
- **Planner benchmark:** compare search time for the current map across the available planners.

## Technology stack

- React 18
- Vite 6
- JavaScript (ES modules)
- CSS
- Lucide React icons

## Run locally

### Requirements

- Node.js 18.18+ (Node.js 20 LTS recommended)
- npm

### Installation

```bash
git clone https://github.com/karanbajaj2057/AutoNav-Sim.git
cd AutoNav-Sim
npm install
npm run dev
```

Open the local URL printed by Vite (usually `http://localhost:5173`).

### Production build

```bash
npm run build
npm run preview
```

The production-ready site is generated in `dist/`.

## How to use

1. Choose an environment preset.
2. Select **Wall**, **Erase**, **Start**, or **Goal** in the map editor. Click or drag to edit cells.
3. Select A*, Dijkstra, Greedy, or BFS.
4. Click **Plan route** to calculate a route and inspect planning metrics.
5. Click **Navigate** to animate the robot along the route. Pause or reset as needed.
6. Use the LiDAR rays toggle and event log to inspect the simulation.
7. Use **Benchmark all planners** to compare search times on the current map.

## Algorithms

| Algorithm | Strategy | Typical trade-off |
|---|---|---|
| A* | Accumulated path cost plus an octile-distance heuristic | Finds a shortest path with the implemented movement costs and heuristic |
| Dijkstra | Accumulated path cost only | Finds a shortest path; may expand more nodes |
| Greedy Best-First | Heuristic distance to goal | Often explores quickly but does not guarantee a shortest path |
| BFS | Breadth-first traversal | Useful for unweighted graphs; here it is included as a comparison baseline |

The simulation uses eight-direction movement. Orthogonal steps cost `1`, diagonal steps cost `√2`, and diagonal movement through blocked corners is prevented. For formal algorithm benchmarking, note that BFS treats edges as equal-depth steps and therefore is not guaranteed to minimize the weighted diagonal path cost.

## Project structure

```text
AutoNav-Sim/
├── public/             # Static assets (add screenshots and favicon here)
├── src/
│   ├── main.jsx        # React application and navigation simulation
│   └── styles.css      # Responsive dashboard styling
├── index.html          # HTML entry point and metadata
├── package.json        # Dependencies and scripts
├── vite.config.js      # Vite configuration
├── .gitignore
├── LICENSE
└── README.md
```

## Screenshots

Add genuine screenshots of your running application to `public/screenshots/`, then embed them here. Suggested captures:

- `dashboard.png` — full navigation dashboard with the Warehouse AMR scenario.
- `route-planned.png` — map with a computed path and telemetry visible.
- `scenario-editor.png` — map editor showing wall placement and scenario presets.

Example Markdown after adding the screenshot:

```md
![AutoNav.sim navigation dashboard](public/screenshots/dashboard.png)
```

## Deployment

You can deploy the Vite build to GitHub Pages, Vercel, or Netlify. For GitHub Pages, configure the Pages workflow/build settings for a Vite static site and ensure the Vite `base` matches the repository path if deploying under `username.github.io/AutoNav-Sim/`.

## Roadmap

- [ ] Add deterministic moving-obstacle simulation and robust live replanning.
- [ ] Add export/import for custom maps.
- [ ] Add repeatable benchmark runs with averaged metrics.
- [ ] Add automated tests for planner correctness and unreachable goals.
- [ ] Add a screen recording or GIF of a complete navigation run.

## Safety note

This is a simplified educational grid simulation. It is not validated for controlling physical robots, autonomous vehicles, or safety-critical equipment.

## Acknowledgements

Built as an educational project to explore robotics, graph search, path planning, simulated perception, and interactive visualization.

## License

Released under the MIT License. See [`LICENSE`](LICENSE).
