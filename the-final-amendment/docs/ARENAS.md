# Arenas

Project Dusk Phase 1 ships one playable industrial deathmatch arena and one stub for rotation testing. All arenas use Meshy.ai modular props with Enhanced GS dark industrial lighting.

---

## Arena Overview

| ID | Scene | Phase | Status |
|----|-------|-------|--------|
| `Industrial_01` | `Arena_Industrial_01` | 1 | **Playable** |
| `Industrial_02` | `Arena_Industrial_02` | 1 | Stub / greybox |

---

## Arena_Industrial_01 — "Scrapyard Pit"

**Display name:** Scrapyard Pit  
**Theme:** Enclosed factory yard — ramps, crates, central toxic pit  
**Mood reference:** Twisted Metal Black industrial / asylum-yard grit (original layout)

### Layout

```
                    ┌─────────────────────────────┐
                    │     N — Spawn row (4)       │
                    │  [S1] [S2] [S3] [S4]        │
                    ├─────────────────────────────┤
                    │  Ramp NW    │    Ramp NE    │
                    │             │               │
     W — Wall       │   Crates    │   Crates      │  Wall — E
     modular        │   + pipes   │   + wreckage  │
                    │             │               │
                    │      ┌───────────┐          │
                    │      │ TOXIC PIT │          │
                    │      │ (damage)  │          │
                    │      └───────────┘          │
                    │  Ramp SW    │    Ramp SE    │
                    ├─────────────────────────────┤
                    │     S — Pickup lane         │
                    └─────────────────────────────┘
```

### Features

| Feature | Description |
|---------|-------------|
| **Central toxic pit** | Damage-over-time volume; visual green glow via `PS2/Water` + particles |
| **Four ramps** | Jump shortcuts; risk landing near pit edge |
| **Crate clusters** | Cover; destructible barrel stubs near NE cluster |
| **Modular walls** | Meshy factory wall segments; limits sightlines |
| **Spawn points** | 4 fixed points (N row); used by humans and bots |
| **Pickup nodes** | 6 fixed respawn locations — health, weapons, turbo |
| **Bounds** | Invisible kill plane below pit; wall colliders on perimeter |
| **Skybox** | Enclosed smog-dome — `PS2/Sky` gradient, no visible horizon |
| **Ambient audio** | Distant machinery loop, toxic bubble SFX near pit |

### Lighting (Enhanced GS)

| Light | Type | Notes |
|-------|------|-------|
| Sun | Directional | Dim, amber-grey — mostly occluded by smog dome |
| Sodium floods | Point (vertex) | 4–6 flickering industrial lamps |
| Pit glow | Point (green) | Toxic pit emissive fake |
| Vehicle headlights | Per-vehicle second pass | Emissive `PS2/Unlit` |

**Profile defaults:** Medium tier, fog 120 m, soot fog color `#2a2218`.

### Pickup Spawn Table

| Node | Default Spawn | Respawn (sec) |
|------|---------------|---------------|
| NW corner | Health | 30 |
| NE corner | Homing | 45 |
| SE corner | Fire | 45 |
| SW corner | Turbo/Nitro | 40 |
| S center | Power | 60 |
| Pit rim (risk) | Special | 90 |

### Match Configuration

```yaml
arenaId: Industrial_01
maxCombatants: 4
matchDurationSeconds: 180
botCount: 3          # Phase 1: 1 human + 3 bots
friendlyFire: false
hazardsEnabled: true
```

### Asset Dependencies (Meshy)

- Industrial wall segments (×8–12 instances)
- Metal ramps (×4)
- Supply crates (×6)
- Explosive barrels (×4)
- Toxic pool edge trim (×1 modular kit)
- Smokestack props (×2 background)

See [MESHY_PROMPTS.md](MESHY_PROMPTS.md) for generation prompts.

---

## Arena_Industrial_02 — "Foundry Loop" (Stub)

**Display name:** Foundry Loop  
**Theme:** Partially open foundry ring — elevated catwalk, molten channel stub  
**Status:** Greybox for rotation testing; duplicate layout placeholder

### Planned Features (Phase 2+)

| Feature | Description |
|---------|-------------|
| **Elevated catwalk** | Second-level route; fall damage stub |
| **Molten channel** | Linear hazard along W side — high DOT |
| **Overhead crane mesh** | Visual only; collision off |
| **Narrow choke tunnel** | Central underpass connecting halves |

Phase 1: scene file exists with flat plane + spawn markers only. Not in Quick Match rotation.

---

## ArenaDefinition ScriptableObject

```csharp
// Assets/_ProjectDusk/Data/Arenas/Industrial_01.asset
public class ArenaDefinition : ScriptableObject
{
    public string arenaId;
    public string displayName;
    public SceneReference scene;
    public Transform[] spawnPoints;      // length 4
    public PickupSpawnNode[] pickups;
    public Bounds arenaBounds;
    public AudioClip ambientLoop;
    public float matchDurationSeconds = 180f;
}
```

---

## Hazards (Shared)

| Hazard | Behavior | Phase |
|--------|----------|-------|
| Toxic pool | 5 DPS while overlapping | 1 |
| Explosive barrel | Chain explosion on weapon hit | 1 (stub) |
| Kill plane | Instant destroy below Y threshold | 1 |
| Molten channel | 10 DPS | 2 |

---

## Future Arena Ideas (Out of Scope Phase 1)

| Concept | Hook |
|---------|------|
| Parking garage stacks | Vertical combat, multi-floor |
| Flood channel | Rising toxic water timer |
| Rooftop helipad | Open sightlines, helicopter pickup stub |

---

## Related Documents

- [MESHY_PROMPTS.md](MESHY_PROMPTS.md) — prop generation prompts
- [ENHANCED_GS_RENDERING.md](ENHANCED_GS_RENDERING.md) — arena lighting and fog
- [ARCHITECTURE.md](ARCHITECTURE.md) — DeathmatchManager and ArenaDefinition
- [MULTIPLAYER.md](MULTIPLAYER.md) — `--arena=` dedicated server flag
