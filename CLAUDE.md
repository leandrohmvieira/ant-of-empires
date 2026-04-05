# Ant of Empires

## Overview
RTS game where players control ant colonies through algorithms rather than direct unit control. Godot 4.4, GDScript. Players write or configure behavioral algorithms that govern ant decision-making — foraging, combat, expansion, resource management — and watch their colony execute autonomously.

## Engine
- Godot 4.4.1 stable
- GDScript only (no C#, no GDExtension)
- Target: PC (Windows/Linux)

## Architecture

### Core Patterns
- **Managers (autoloads)** own game systems. Nodes are views only.
- **Resources (.tres)** hold data and state — not nodes.
- **Signals** for communication between managers — never direct calls.
- **Component-based design** — prefer composition over inheritance.

### Key Systems
- **ColonyManager** — Colony state, population, resources
- **AlgorithmManager** — Player-defined behavioral rules, algorithm execution
- **MapManager** — Terrain, tiles, pheromone trails, food sources
- **SimulationManager** — Tick-based simulation loop, ant AI stepping
- **CombatManager** — Colony vs colony and colony vs environment encounters
- **UIManager** — HUD, algorithm editor, colony stats, minimap

### Simulation Model
- Tick-based simulation (not frame-based) — game logic runs on fixed ticks
- Ants are lightweight entities (data in Resources), not individual nodes
- Pheromone system for pathfinding and communication between ants
- Algorithm evaluation happens per-tick per-ant-group, not per-frame

## Directory Structure
```
res://
  scenes/           # .tscn scene files
    ui/             # UI scenes
    world/          # Map, terrain, colonies
    entities/       # Ant visual representations
  scripts/          # .gd script files
    autoloads/      # Manager singletons
    entities/       # Ant, colony, food logic
    algorithms/     # Algorithm system, built-in behaviors
    systems/        # Pheromone, pathfinding, combat
    ui/             # UI controllers
  resources/        # .tres custom resources
    algorithms/     # Algorithm definition resources
    entities/       # Ant type definitions, colony configs
    map/            # Terrain, biome data
  assets/
    sprites/        # 2D art, ant sprites, terrain tiles
    audio/          # SFX, music
    fonts/          # UI fonts
    shaders/        # Visual effects
  data/             # JSON/config for balance values
    balance.json    # All tuning values — never hardcode these
  tests/            # GdUnit4 test files
```

## Conventions

### GDScript Style
- `PascalCase` for classes and nodes
- `snake_case` for functions, variables, signals
- `UPPER_SNAKE_CASE` for constants and enums
- Type hints on everything: `var speed: float = 10.0`
- `@onready` for node references, `@export` for inspector variables
- `%UniqueNode` or `@onready` for node refs — never hardcoded `get_node()` paths
- One class per file, `class_name` at the top
- Signals named in past tense: `colony_founded`, `ant_died`, `resource_gathered`

### Scene/Resource Files
- `.tscn`/`.tres` files must NOT contain GDScript syntax
- Use `ExtResource("id")` in scene files, not `preload()`
- Use typed arrays `Array[Type]([...])` in resource files

### Code Organization
- Game logic in scripts, visual representation in scenes
- Balance values in `data/balance.json` only — never hardcode numbers
- Algorithms are data-driven (Resources), not hardcoded scripts

## Anti-Patterns — Do NOT
- Put game state in nodes — use Resources or autoloads
- Use physics engine for game logic — this is a simulation, not physics-based
- Use `await` in `_ready()`
- Call between managers directly — use signals
- Add new autoloads without asking
- Hardcode balance values — put them in `data/balance.json`
- Create individual Node2D per ant — ants are data, render them in batches
- Mix simulation logic with rendering — keep them separated

## Build & Run
- Run project: open `project.godot` in Godot Editor, press F5
- Run specific scene: F6 in editor with scene open
- Tests: GdUnit4 plugin (run from editor or CLI)
- Formatting: `gdformat` for code style
- Linting: `gdlint` for static analysis

## Game Design Notes
- Ants are grouped by role (forager, soldier, builder, scout) — algorithms assign roles
- Resources: food, building material, larvae
- Pheromone trails decay over time and guide ant navigation
- Multiple colonies can exist on one map — PvE and PvP scenarios
- Win conditions: eliminate rival colonies or reach population/resource thresholds
