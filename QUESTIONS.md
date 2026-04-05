# Ant of Empires — Design Questions

Decisions to make before building v1.

## Visual & Rendering
1. **2D or 3D?** — Top-down 2D, isometric 2.5D, or full 3D?
2. **Camera** — Fixed, pannable, zoomable? What's the default view scale?
3. **Art style** — Pixel art, vector, realistic? Placeholder sprites ok for v1?
4. **Ant rendering** — MultiMeshInstance2D for batch rendering? How many ants on screen at once (100s? 1000s?)
5. **Map visuals** — TileMap-based terrain? Procedurally generated or hand-crafted?

## Map & World
6. **Map size** — Small arena or large world? Grid-based or continuous coordinates?
7. **Tile types** — What terrain exists? (dirt, rock, water, food sources, nest entrances)
8. **Procedural generation** — Random maps, seed-based, or designed levels?
9. **Fog of war** — Can you see the whole map or only where your ants have explored?

## Simulation
10. **Tick rate** — How many simulation ticks per second? Adjustable speed (1x, 2x, 5x)?
11. **Ant count** — Max ants per colony for v1? (affects architecture choices)
12. **Pheromone model** — Grid-based pheromone map? Resolution? Decay rate?
13. **Pathfinding** — A* on grid? Pheromone-following only? Hybrid?

## Algorithm System (the core mechanic)
14. **How do players define algorithms?** — This is THE key question:
    - Visual node graph (like Godot's VisualScript was)?
    - Priority list / behavior tree editor?
    - Simple rule cards (IF food nearby THEN gather)?
    - Actual scripting (sandboxed GDScript/custom DSL)?
    - Preset algorithms with tunable parameters?
15. **Algorithm granularity** — One algorithm per colony? Per role? Per individual ant?
16. **What inputs can algorithms read?** — Nearby food, pheromone strength, enemy proximity, colony resources, ant health?
17. **What actions can algorithms output?** — Move, gather, attack, lay pheromone, return to nest, recruit?
18. **Real-time editing?** — Can players modify algorithms while the simulation runs?

## Gameplay
19. **Single player first or multiplayer?** — v1 scope
20. **Win condition for v1** — Eliminate enemy? Gather X food? Survive N minutes?
21. **Enemy AI** — Pre-built algorithm sets? Difficulty levels?
22. **Resources** — Just food for v1, or food + building material + larvae from the start?
23. **Ant roles for v1** — All roles (forager, soldier, builder, scout) or start with just forager + soldier?
24. **Colony building** — Can ants dig tunnels / expand the nest, or is the nest just a spawn point?

## UI
25. **Algorithm editor placement** — Sidebar panel? Separate screen? Overlay?
26. **What stats are visible?** — Population, food, ant distribution, pheromone overlay toggle?
27. **Minimap** — Needed for v1?

## Scope for v1
28. **What's the minimum playable version?** — e.g., "one colony, food foraging only, preset algorithms with parameter sliders, single map"
29. **What gets cut from v1?** — Combat? Multiple colonies? Custom algorithms?
