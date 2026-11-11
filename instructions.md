# THE HOLLOW — MULTI-REALM WORLD SYSTEM & VERTICAL EXPLORATION

## Project vision

We are evolving THE HOLLOW into a much larger multi-world exploration and survival game.

Study the existing game carefully before making changes.

We have an existing game and working mechanics that must be preserved. We are not starting from scratch.

### Reference project: SkyJump3D

Repository:
https://github.com/Chimthuwu/SkyJump3D

Use these specific systems as design references:

- `index.html` — `ZONES`, `setZone()`, `dressSite()`, `buildBackdrop()` and `updateWorlds()`: biome and environmental design.
- `index.html` — `ladderExtend()`, `ladderBot`, `ladderTop` and `updateLadderLabels()`: endlessly extending vertical platform progression.
- `index.html` — `buildSkyway()`: ascending platform route leading to the Moon.
- `index.html` — `buildAlienRoute()`: multi-lane progression through space towards Mars.
- `index.html` — `addPortal()`, `unlockPortal()` and `updatePortals()`: discoverable portal system.
- `PERFORMANCE_AUDIT.md`: documented performance, architecture and memory problems.

Do not copy the implementation blindly. Understand what each system accomplishes and adapt the successful concepts to THE HOLLOW.

---

# 1. THE NEW WORLD STRUCTURE

THE HOLLOW is the name of the game, but The Hollow itself will become one of its separate dimensions.

The player should start in a more familiar, welcoming floating-island environment.

## Starting realm: THE DRIFT

Working name; can be changed if a better name is found.

This is the default starting world.

It should feature:
- Beautiful floating islands.
- Grass, soil, trees and natural vegetation.
- Waterfalls and floating water features.
- Ruins and ancient structures.
- Distinct island environments.
- Wildlife and exploration.
- A relatively welcoming atmosphere.
- Mysterious discoveries suggesting other dimensions exist.

It should feel like a genuine world that the player wants to explore, not merely a tutorial island.

Preserve the floating-island identity of the existing game.

## Darkness realm: THE HOLLOW

The existing horror environment becomes a separate dark dimension.

It should have:
- Dark floating islands.
- Corrupted landscapes.
- Strange forests.
- Abyssal structures.
- Oppressive atmospheric effects.
- Disturbing creatures.
- Unusual environmental hazards.
- Different survival conditions from The Drift.

The Hollow should feel substantially different from the starting realm.

It must be a proper explorable world, not simply The Drift with a darker colour filter.

## Future realm destinations

Design the architecture to support additional dimensions, including concepts such as:

- LUCID GARDEN — psychedelic forests, enormous plants, vivid colours, unusual organic life and dreamlike landscapes.
- THE GLASS SEA — floating oceans, suspended waterfalls and crystalline formations.
- THE INVERTED — impossible architecture, upside-down islands and gravity anomalies.
- THE AMBER DREAM — golden skies, strange celestial phenomena and ancient crystal landscapes.
- THE UNDERWORLD — deeper layers beneath the darkness realm, eventually leading towards a Hell-like environment.

These are future content directions. Do not try to build them all immediately.

The system must make adding a new realm straightforward.

---

# 2. A REAL MULTI-REALM ARCHITECTURE

Create a reusable realm system inspired by SkyJump3D's biome registry, but with a more substantial separation between worlds.

A realm should have its own:

- Unique identifier.
- Display name and description.
- World seed.
- Terrain and island generation.
- Environmental settings.
- Sky and lighting.
- Fog and atmosphere.
- Weather.
- Ambient audio.
- Biome definitions.
- Vegetation and architectural styles.
- Creature population.
- Resource distribution.
- Gameplay modifiers.
- Gravity and movement conditions where appropriate.
- Entry points and return points.
- Vertical progression configuration.
- Portal destinations.
- Persistent save state.

Keep individual biomes inside realms.

For example, The Drift might contain forests, grasslands, rocky islands and frozen high-altitude regions. These are biomes within one realm, not necessarily separate dimensions.

Likewise, The Hollow could contain corrupted forests, dark ruins and abyssal regions.

**Worlds and biomes must be different systems.**

Do not implement realms by repeatedly calling the existing biome-changing function.

---

# 3. THE VERTICAL WORLD — A MAJOR GAMEPLAY FEATURE

This is one of the most important aspects of the entire project.

I want to recreate and improve the vertical exploration concept from SkyJump3D.

The player must be able to explore both above and below the main floating world.

This should feel like an interconnected vertical universe.

## A. The downward journey

The starting realm must have a meaningful lower boundary.

Below the main floating islands, the player discovers increasingly unusual environments.

Create a vertical descent system inspired by SkyJump3D's numbered platform ladder.

Concept:

1. The player discovers a route beneath the starting islands.
2. They descend through increasingly distant floating platforms.
3. They reach the lowest currently generated platform.
4. Reaching the frontier generates another navigable section below.
5. They continue deeper into the unknown.
6. The environment gradually transforms as they descend.
7. Eventually they reach a major dimensional transition into The Hollow.

The descent should have distinct environmental stages rather than endless identical platforms.

Possible progression:
- Lower floating islands.
- Hanging forests and enormous roots.
- Broken ruins suspended in the void.
- Deep atmospheric cloud layers.
- Strange geological formations.
- Corrupted and increasingly unfamiliar environments.
- The boundary into The Hollow.
- Deeper abyssal layers.
- Eventually the Underworld and Hell-like regions.

The descent should feel like travelling somewhere.

It should not just be a teleport to a randomly generated black platform field.

## B. The upward journey

The player should also be able to climb beyond the highest parts of the starting realm.

Create an upward progression system inspired by SkyJump3D's skyway and Moon route.

Concept:

1. Discover an ascent route.
2. Climb through elevated floating islands.
3. Reach higher atmospheric environments.
4. Pass through clouds and increasingly unusual sky formations.
5. Discover abandoned structures and platforms suspended above the atmosphere.
6. Reach an orbital region.
7. Eventually discover the Moon.
8. Later unlock further space exploration.

The Moon should be a genuine destination with its own environment and exploration opportunities.

Beyond the Moon, the architecture must support:
- Orbital structures.
- Asteroids.
- Alien environments.
- Space stations.
- Strange celestial worlds.
- Further planetary destinations.

Do not build a thousand platforms merely to create distance.

Focus on interesting routes, meaningful discoveries and a sense of scale.

## C. Vertical progression must be expandable

The player should not reach a hard-coded final platform and discover that there is nowhere else to go.

Build a reusable frontier-generation system.

It must support:
- Extending upward.
- Extending downward.
- Creating new navigable platform sections.
- Different environmental themes depending on depth or altitude.
- Unique landmarks and destinations.
- Controlled progression and unlocks.
- Deterministic generation.

Use a consistent system for numbering or identifying generated sections if it helps track vertical progression.

Most importantly, make this system work without allowing the world to grow indefinitely in memory.

---

# 4. PORTALS AND INTER-DIMENSIONAL TRAVEL

Integrate the portal concept from SkyJump3D, but develop it into a proper multi-realm travel system.

Portals should be physical objects discovered in the environment.

Some can be:
- Ancient arches.
- Strange dimensional gateways.
- Floating rings.
- Ruined structures.
- Organic portals.
- Unstable energy formations.

Each portal must know its destination realm and destination spawn anchor.

Do not rely on fragile hard-coded world coordinates.

### Portal behaviour

- Some portals begin dormant.
- Players discover and activate them through exploration.
- Active portals visually communicate their destination.
- Travelling through them creates a smooth transition.
- Every destination has a safe arrival point.
- Return travel must work.
- Some destinations may require progression or specific discoveries.
- Previously discovered portals can become accessible through a central gateway network.

The central Nexus concept can be introduced later. Do not make it compulsory if discovered physical gateways provide a better experience.

### Preserve world state

When travelling between realms:
- Preserve player inventory.
- Preserve character progression.
- Preserve health and relevant player state appropriately.
- Save the origin realm and portal.
- Record the player's previous position.
- Remember world modifications.
- Remember gathered resources and discovered locations.
- Return the player to the correct place when using the return portal.

Do not reset a destination every time the player visits it.

---

# 5. WORLD GENERATION AND PERSISTENCE

Create a reliable foundation for multiple independently generated environments.

Each realm should have a stable seed.

Generation should be deterministic.

Use separate seeded random streams for:
- Terrain and island layout.
- Environmental dressing.
- Resources.
- Structures.
- Creatures.
- Vertical route generation.
- Decorative effects.

This prevents adding a few decorative objects from unexpectedly changing the entire world layout.

Each realm needs persistent state.

At minimum, save:
- Its seed.
- Discovered locations.
- Opened portals.
- Collected resources.
- Player-built structures.
- Changed or destroyed objects where persistence matters.
- World-specific progression.
- Current entry and return anchors.

Use a versioned save format with sensible validation and recovery.

Maintain compatibility with existing THE HOLLOW saves wherever practical.

Do not silently discard old player progress.

---

# 6. STREAMING AND PERFORMANCE

This is where we must learn from SkyJump3D.

Do not repeat the approach of continually adding more and more objects into one enormous scene.

Use a sensible chunk or region streaming architecture.

Requirements:
- Generate new route sections ahead of the player.
- Keep a controlled number of nearby sections active.
- Unload distant decorative objects and inactive content safely.
- Preserve persistent changes when a region is unloaded.
- Cache reusable geometry and materials.
- Use InstancedMesh where appropriate.
- Use spatial partitioning for collision and proximity checks.
- Avoid scanning every object in the world every frame.
- Avoid repeatedly rebuilding existing terrain.
- Dispose geometries, materials, textures and render targets when appropriate.
- Avoid unbounded arrays and scene-graph accumulation.

Do not preload every realm.

Only keep the current realm and necessary adjacent content active.

Use lazy generation for expensive destinations such as the Moon, space regions and deeper dimensions.

Generation must not freeze gameplay.

Introduce incremental generation, loading transitions or background preparation where appropriate.

---

# 7. GENERATION MUST PRODUCE PLAYABLE ROUTES

This is especially important.

SkyJump3D's vertical platform ladder was an exciting concept, but simply generating random platforms around a centre point does not guarantee a good route.

For THE HOLLOW:

- Generate intentional navigable paths.
- Validate jump distances and elevation changes.
- Account for the actual movement, jump and glide capabilities.
- Ensure important routes are physically reachable.
- Allow optional branches and shortcuts.
- Prevent platforms spawning inside one another.
- Avoid paths that lead to unavoidable deaths.
- Ensure portals never spawn in inaccessible locations.
- Ensure every portal has a valid destination or a clear reason to remain dormant.
- Ensure the player can always return from a destination unless an intentional one-way progression event is clearly communicated.

Have the generation system validate its own route graph before presenting it to the player.

Do not mistake an absence of JavaScript errors for proof that the world is playable.

---

# 8. PROGRESSION AND DISCOVERY

Make vertical exploration meaningful.

The player should discover:
- New realms.
- New resources.
- New creatures.
- New crafting materials.
- Unique structures.
- New environmental mechanics.
- Rare equipment.
- Unlockable destinations.
- Lore and clues about the relationship between dimensions.

The player should gradually understand that the worlds are connected.

The Hollow should be an important discovery, not simply an alternative starting location.

The Moon and space should feel like major exploration achievements.

The Underworld should be a significant descent milestone.

Do not introduce complicated progression systems with no practical gameplay purpose.

---

# 9. DEVELOPMENT PITFALLS — READ CAREFULLY

Use SkyJump3D as a source of design inspiration, but do not repeat its engineering problems.

### Avoid monolithic code growth

SkyJump3D developed into a very large single-file application.

THE HOLLOW must not become an increasingly unmaintainable file containing every realm generator, portal mechanic, resource system and environment update.

Inspect the existing architecture and create clear system boundaries.

If the existing project is currently a single HTML file, do not blindly force a massive framework migration. Make a deliberate technical decision and preserve the ability to run and deploy the game.

### Avoid parallel editing conflicts

Do not assign multiple agents to simultaneously modify the same large source file.

Use distinct file ownership, isolated modules and clear integration points.

### Avoid procedural feature bloat

Do not generate thousands of platforms and hundreds of enemies just because the generator can.

World size must be justified by interesting places to visit.

### Avoid memory leaks

Every realm and streamed region must have a lifecycle.

Unloading a region must remove its objects from the scene and properly release resources that are no longer referenced.

### Preserve determinism

A realm's layout must remain consistent when regenerated from the same seed.

Do not allow decorative randomness to alter gameplay-critical generation.

If multiplayer exists in the current game, preserve the established authority and synchronisation model.

### Verify real traversal

Test actual movement through the generated routes.

Test downward and upward progression.

Test portal travel and return travel.

Test saving and reloading after changing realms.

### Don't replace working systems

Inspect THE HOLLOW's existing movement, physics, crafting, survival, building, inventory, sanity and interaction code.

Preserve functioning mechanics.

Do not remove or rewrite them merely to make the realm system easier to implement.

---

# 10. IMPLEMENTATION APPROACH

Do not attempt to build the entire universe in one pass.

Start with a focused, fully functioning vertical slice.

## Stage 1 — Architecture and foundation

- Inspect the existing THE HOLLOW codebase.
- Map its existing world-generation and gameplay systems.
- Review its save/load implementation.
- Identify integration points for portals and realm state.
- Study the SkyJump3D references above.
- Record the specific lessons and risks.
- Design the smallest maintainable realm architecture.

Do not spend excessive time producing a giant theoretical design document.

Make the architectural decisions and implement them.

## Stage 2 — The Drift

Make The Drift the initial playable realm.

Preserve the existing floating-island gameplay, but establish its role as the default, more welcoming world.

Create its initial environment, starting location and exploration routes.

## Stage 3 — Vertical exploration

Implement the expandable vertical route system.

Both upward and downward exploration must be supported.

Build a working route that demonstrates that the player can continue exploring beyond the original generation boundary.

The downward route should lead towards the entrance to The Hollow.

The upward route should ultimately support travel to the Moon and beyond.

## Stage 4 — The Hollow

Integrate the existing dark environment as a separate realm.

Preserve its distinctive horror mechanics and atmosphere.

Implement a working portal or dimensional transition from the starting world.

Make return travel reliable.

## Stage 5 — Persistence and quality assurance

Verify:
- Realm loading and unloading.
- Portal activation.
- Travel between realms.
- Return travel.
- Save/load across realms.
- Deterministic regeneration.
- Upward and downward route extension.
- Route connectivity.
- Collision reliability.
- Memory disposal.
- Performance.

Only after the first slice works should the additional realms be expanded.

---

# 11. ACCEPTANCE CRITERIA

The first implementation is complete when:

1. The player starts in The Drift, not The Hollow.
2. The existing Hollow environment is accessible as a separate darkness realm.
3. A real, usable portal connects the two realms.
4. The player can return to their original realm and location.
5. Player inventory and progression survive realm transitions.
6. Realm state persists across save/load.
7. The game supports independently seeded realm generation.
8. A downward platform route can extend beyond its original boundary.
9. An upward platform route can extend beyond its original boundary.
10. The vertical routes are physically traversable.
11. Expensive realm content is not all loaded simultaneously.
12. Repeated transitions and world generation do not create unbounded memory growth.
13. Existing THE HOLLOW gameplay remains functional.

The Moon, deeper Underworld, Hell and further space destinations must have clear architectural support, even where they are not fully developed in this first implementation.

The final report must distinguish implemented, tested and still-planned features.

---

# FINAL DIRECTION

We want the sense of scale and vertical discovery that made SkyJump3D interesting.

But we want to do it with better world architecture, more deliberate environments, more interesting routes, persistent dimensions and far better performance.

The player should be able to look up and wonder what is above them.

They should be able to look down and wonder how deep the world goes.

They should discover portals and realise there are completely different dimensions waiting to be explored.

**THE HOLLOW is no longer just one floating world. It is a universe of connected worlds, with an enormous vertical frontier above and below.**

Build the foundation properly. Make the first slice genuinely playable. Then expand it without sacrificing the quality or stability of the original game.