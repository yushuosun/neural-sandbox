# Neural Sandbox

**Fifteen interactive AI demos — evolution, optimization, learning, diffusion, chaos, emergence, search, and more — running entirely in your browser.**

🔗 **Live:** https://yushuosun.github.io/neural-sandbox/

No frameworks. No build step. No external dependencies. Every demo is a single, self-contained `index.html` you can read top to bottom — the neural networks, backprop, diffusion sampler, and physics are all written from scratch in plain JavaScript.

---

## The demos

| Demo | What it does | Category |
|---|---|---|
| [Foragers](demos/foragers/index.html) | Tiny neural brains evolve to hunt food and flee predators | Artificial Life |
| [Optimizers Arena](demos/optimizers/index.html) | Five optimizers race across a 2D loss landscape | Optimization |
| [Neural Playground](demos/playground/index.html) | Draw your own data, watch an MLP learn the boundary live | Interactive ML |
| [Diffusion Lab](demos/diffusion/index.html) | A tiny net turns noise into shape — DDPM made visible | Generative Models |
| [Reaction-Diffusion Studio](demos/reaction-diffusion/index.html) | Paint Gray-Scott Turing patterns in real time | Generative Art |
| [Boids](demos/boids/index.html) | Three local rules, one flock, no leader | Swarm Intelligence |
| [Automata Lab](demos/automata/index.html) | Cellular automata — Life, HighLife, Maze, and more | Emergence |
| [Strange Attractors](demos/attractor/index.html) | Lorenz / Clifford / De Jong chaos, drawn live | Chaos & Dynamics |
| [RL Playground](demos/rl-gridworld/index.html) | A Q-learning agent learns the shortest path live | Reinforcement Learning |
| [K-Means Lab](demos/kmeans/index.html) | Scatter points, drop centroids, watch clusters form | Interactive ML |
| [Wave Function Collapse](demos/wave-collapse/index.html) | Coherent patterns from constraint propagation | Procedural Generation |
| [Fourier Epicycles](demos/fourier/index.html) | Any closed path as a sum of spinning circles | Signals & Math |
| [Slime Mold](demos/slime-mold/index.html) | Physarum agents grow a living network (stigmergy) | Artificial Life |
| [Genetic TSP](demos/genetic-tsp/index.html) | A genetic algorithm untangles the salesman route | Evolutionary Optimization |
| [Pathfinding Visualizer](demos/pathfinding/index.html) | A* / Dijkstra / BFS / Greedy race across a grid | Search Algorithms |

---

### 🧬 Foragers — neuroevolution
Each agent carries a genome decoded into a small feed-forward network: 7 raycast vision sensors (nearest food / predator / wall) plus its own velocity feed 8 tanh hidden units that output steering and thrust. Every generation, the fittest are kept (elitism + top-30% breeding) and reproduced with Gaussian mutation. Foraging and predator-avoidance **emerge purely from selection pressure** — there is no hand-written behaviour.
*Where it goes:* a minimal sandbox for evolutionary robotics / open-ended evolution — extend toward NEAT topology evolution or predator–prey co-evolution.

### 📉 Optimizers Arena — optimization intuition
Each terrain (Rosenbrock, Saddle, Himmelblau, Rastrigin, Beale) defines an analytic loss **and** its exact gradient. Five optimizers (SGD, Momentum, NAG, RMSProp, Adam) start from the same draggable point with standard hyperparameters and leave fading trails, with each one's live loss in the legend. The clearest way to *feel* why ravines, saddles and local minima behave the way they do.
*Where it goes:* drop in Lion / second-order methods, plot convergence curves, or slice a real network's loss surface.

### 🎨 Neural Playground — learn by drawing
Paint class A and class B points anywhere in `[-1, 1]²` and a from-scratch MLP (configurable depth, tanh/relu) trains live via hand-written backprop. The decision surface is rendered as a smooth heatmap that updates as the loss and accuracy curves tick down.
*Where it goes:* an explainability sandbox — visualize per-neuron features, add regularization/optimizer comparisons, or load a CSV.

### 🌀 Diffusion Lab — noise → shape
Pick a target point cloud (two moons, spiral, smiley, "AI", ring). A `2→64→64→2` MLP with a sinusoidal time embedding trains on the DDPM ε-objective (from-scratch autograd + Adam), then sampling runs the reverse process and you **watch the cloud condense from noise into the shape**. The forward (noising) process is animated too.
*Where it goes:* DDIM sampling, classifier-free guidance, score-field visualization, beta-schedule ablations.

### 🧫 Reaction-Diffusion Studio — Turing patterns
A Gray-Scott simulation on a grid (typed arrays + ping-pong double buffering, 9-point Laplacian, explicit Euler). Presets produce coral, mitosis, spots, and labyrinths; paint to seed, recolor with palettes, and export a PNG.
*Where it goes:* a morphogenesis teaching tool or a seamless-texture / pattern generator (GPU port for bigger grids).

### 🐦 Boids — emergence from three rules
Separation, alignment, and cohesion over a perception radius, with a spatial-hash grid so 200+ boids stay at 60fps. Toggle a mouse predator, trails, and edge wrap. A textbook case of collective behaviour from purely local interactions.
*Where it goes:* swarm robotics / drone-formation / crowd-simulation sandbox, or a WebGL particle version for tens of thousands of agents.

### 🔲 Automata Lab — emergence from simple rules
A double-buffered `Uint8Array` grid steps a configurable `B/S` rule (Life `B3/S23`, HighLife, Maze, Seeds, Replicator…) on a toroidal board, rendered via an offscreen `ImageData` blitted with nearest-neighbour scaling so tens of thousands of cells stay at 60fps. Paint cells, drop a Gosper glider gun, and watch order emerge from a handful of live cells.
*Where it goes:* a "from discrete to continuous life" teaching series (Langton's Ant, Wireworld, Lenia), a rule-space explorer that scores rules by entropy (novelty search), or a Turing-complete "build logic gates from gliders" tutorial.

### 🌌 Strange Attractors — deterministic chaos
Iterates 2D maps (Clifford, De Jong) and integrates 3D ODEs (Lorenz, Halvorsen) with RK4, accumulating tens of thousands of points per frame with additive `lighter` blending so dense regions glow; colour follows local velocity. NaN/divergence is clamped back to a safe seed so it never blanks.
*Where it goes:* a generative-art engine (high-res export, preset gallery), an audio visualizer / dynamic-wallpaper module, or a dynamical-systems teaching tool for sensitivity-to-initial-conditions and Lyapunov exponents.

### 🎯 RL Playground — value spreads, policy emerges
Tabular Q-learning on a gridworld: `Q(s,a)` in a `Float64Array`, ε-greedy exploration, TD update `Q(s,a) ← Q(s,a) + α·[r + γ·maxₐ′Q(s′,a′) − Q(s,a)]`. The state-value heatmap, greedy-policy arrows, and agent trajectory update live as it learns the shortest path; click to place walls, traps, or move the goal.
*Where it goes:* a comparison bench for SARSA / Double-Q / Dyna / reward-shaping, or an interactive RL-course component that makes Bellman updates visible.

### 🎯 K-Means Lab — clusters crystallize
Lloyd's algorithm live: scatter points (or generate Gaussian blobs), seed `k` centroids (random or k-means++), then iterate assign → update while a downsampled Voronoi background shows each centroid's territory and `inertia` falls to convergence.
*Where it goes:* elbow/silhouette curves for choosing `k`, random-vs-k-means++ restart variance, or GMM/DBSCAN comparisons on non-spherical clusters.

### 🌀 Wave Function Collapse — order from constraint
Each cell starts as a superposition of all tiles; the solver repeatedly observes the lowest-entropy cell, collapses it, and propagates adjacency constraints outward (with restart-on-contradiction). Coherent structure emerges from local rules — a tangible intro to constraint satisfaction.
*Where it goes:* overlapping-model WFC (learn rules from a sample image), backtracking instead of restart, or game level/texture generation.

### 〰️ Fourier Epicycles — a path is a sum of circles
Draw a closed curve (or pick a preset); a from-scratch DFT turns it into a chain of rotating circles (frequency = speed, amplitude = radius, phase = start), tip-to-tail, whose pen tip redraws the original exactly.
*Where it goes:* a frequency-spectrum sidebar, SVG/signature import, low/high-pass filtering (the JPEG/MP3 idea), or an FFT upgrade for thousands of points.

### 🦠 Slime Mold — stigmergy in action
Thousands of minimal agents each sense a shared trail field at three forward sensors, steer toward the strongest scent, move, and deposit more trail; the field diffuses and decays each frame. Out of pure local deposit-attract-decay feedback, a Physarum-like foraging network self-organizes — no central control.
*Where it goes:* food-source attractors (the maze-solving / Tokyo-rail experiments), multi-species competition, or a WebGL/WebGPU port for millions of agents.

### 🧬 Genetic TSP — evolution untangles the route
Each individual is a full tour (a permutation); fitness is `1 / length`. Tournament selection, ordered crossover (OX), swap/reversal mutation, and elitism evolve a tangled random route into a near-optimal loop, with a live best-distance convergence curve.
*Where it goes:* 2-opt/Lin-Kernighan hybrids, island models, TSPLIB import, or VRP/time-window variants.

### 🧭 Pathfinding Visualizer — search, side by side
A*, Dijkstra, BFS, and Greedy Best-First all expand from the start; the difference is *who expands next*. Watch visited cells, the frontier, and the reconstructed shortest path, with manhattan/euclidean (octile for diagonals) heuristics, wall drawing, and maze generation — and compare how much each algorithm explores.
*Where it goes:* weighted terrain, Jump Point Search / D* Lite, bidirectional search, or real road-network navigation.

---

## Run locally

Every demo is static — just open the file, or serve the folder:

```bash
git clone https://github.com/yushuosun/neural-sandbox.git
cd neural-sandbox
python -m http.server 8000   # then open http://localhost:8000
```

## Notes

- **Zero dependencies.** No CDN, no fonts, no libraries — works fully offline.
- **From scratch.** Forward/backprop, the diffusion sampler, the optimizers and the physics are all hand-written, not pulled from a framework.
- Tested for numerical stability (NaN/explosion guards), responsive layout, and `devicePixelRatio` rendering.

## License

[MIT](LICENSE) © 2026 Yushuo Sun
