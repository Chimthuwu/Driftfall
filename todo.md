# PLATFORMR2 (The Drift & The Hollow)
## Stage 1: Architecture and Foundation

### Codebase & Systems Mapping
- **World Generation:** Driven by `generateWorld(seed)` using `REGION_DEFS` and `POI_DEFS`. Generates mathematical locations for islands (x,y,z,w,d,h) and connects them with bridges. Meshes are built separately via `buildIslandMeshes`.
- **Gameplay Systems:** Voxel-based movement with `onGround` and `coyote` time. Resource harvesting and simple gridless building (platforms, ramps, walls) via `buildings` array. Combat with hitscan `updateProjectiles` and a generic enemy pool.
- **Save/Load:** `localStorage` JSON serialization. Previously saved global `gameState.world` and arrays of state. 

### Realm Architecture (Implemented)
- **`REALMS` Object:** Contains configuration for each realm (`drift`, `hollow`), including fog/sky colors, lighting intensities, regions, and POIs.
- **State Segregation:** `gameState.realmsData` caches the state of inactive realms (buildings, harvested nodes, opened caches, world layout, discovered POIs).
- **`switchRealm(realmId)`:** 
  1. Serializes current realm state into `realmsData`.
  2. Updates environment (lighting/fog).
  3. Clears physical scene meshes (`buildingGroup`, `islandGroup`, etc.).
  4. Restores target realm from `realmsData` (or generates fresh).
  5. Teleports player to the target portal or realm origin.
- **Save Integration:** `activeRealmData` is packed into the save file alongside `realmsData` to ensure seamless resumption in the current realm.
- **Portals:** Special POI types (`drift_arch` and `hollow_arch`) that act as reciprocal trigger volumes, executing `switchRealm` when the player enters their radius.

### Lessons & Risks (from SkyJump3D and The Hollow)
- **State Leakage:** The biggest risk when switching realms is leaving active entities, building colliders, or UI elements behind. **Mitigation:** We rigorously clear `scene` groups, `gameState.buildings`, `gameState.entities`, `gameState.rewardCaches`, and rebuild them from `realmsData`.
- **Performance:** Keeping all realms in memory as THREE.js meshes would crash the browser. **Mitigation:** `switchRealm` destroys the THREE.js meshes for the old realm and only retains the lightweight JS object representations, rebuilding meshes only on entry.
- **Fall Loops:** Vertical exploration requires a kill floor. If a player falls in *The Drift*, they shouldn't just die—perhaps they fall into *The Hollow*. For now, the standard `y < -50` kill plane applies, but cross-realm falling is a future architectural consideration.
- **Light & Environment Leaks:** THREE.js materials (like `FogExp2`) need explicit color/density updates when switching dimensions. **Mitigation:** `applyRealmEnvironment()` mutates the global lights and fog dynamically.

### Stage 2 & 3: Verticality (Implemented)
- **Ascension:** Added `drift_peak` POI at `y: 160` (The Drift Peak). It is a large, high-altitude tower requiring player building to scale, rewarding them with a citadel cache. This fulfills the upward exploration route.
- **Descent (The Fall):** Falling off the edge in The Drift (`y < -75`) no longer damages or resets you; instead it automatically switches the realm to `hollow` and drops you into the dark sky, maintaining your X/Z coordinates. This acts as the dramatic downward route connecting the realms.

### Stage 4 & 5: The Hollow and QA (Implemented)
- **Realm loading/unloading:** Rebuilt the `checkPortalInteraction` logic to ensure precise dimensional transitions using collision volumes (`dx*dx + dz*dz < radius*radius`).
- **Save/Load validation:** Fully validated saving states containing both `activeRealmData` (e.g. your active progress in The Drift) and `realmsData` (your cached buildings/resources in The Hollow). The save file successfully parses and re-initializes upon refresh (`btn-continue`).
- **Portal & Return Travel:** `drift_arch` connects down into The Hollow, and `hollow_arch` successfully connects back to The Drift.

## 2026-11-12: Rename + ship
- CRITICAL FIX: commit 166085e (skybox swap) left an orphaned silhouette block with a stray `}` after `updateSkybox()` — module-level SyntaxError, game never started (black screen, HUD static HTML only). Fixed by removing the stray brace (silhouettes now build once at top level into `scene`).
- Renamed to DRIFTFALL (The Hollow is now just one realm). og:/twitter: meta + thumb.png (1200x630 in-game capture, HUD hidden) + favicon.png.
- Live: https://driftfall-237.pages.dev · Repo: github.com/Chimthuwu/Driftfall · Cloudflare Pages project `driftfall` (manual `wrangler pages deploy . --project-name=driftfall`).
- og:image hardcoded to driftfall-237.pages.dev — update if a custom domain is added.
