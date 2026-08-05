# Phase 2 — Local Couch Multiplayer

Phase 2 adds **2–4 human players on one machine** with split-screen cameras, per-slot input, and bot-filled remaining slots.

## Menu flow

```
Main Menu
├── Quick Match        → offline 1 human + 3 bots
└── Local Multiplayer  → LocalMatchSetup (pick 2/3/4 players) → Vehicle Select → Arena
```

## New / updated systems

| System | Role |
|--------|------|
| `MatchConfig.CreateLocalCouch(n)` | 2–4 humans, fills to 4 combatants with bots |
| `GameSession.ApplyMatchConfig()` | Persists config + configures `PlayerSlotRegistry` |
| `LocalMatchSetupController` | Player count selection UI |
| `DeathmatchManager` | Slot-based spawn, elimination win, `MatchEnded` event |
| `LocalMatchRuntime` | Device routing, per-human input, split-screen cameras, HUD |
| `SplitScreenLayout` | Viewport rects for 1–4 players |
| `CombatVehicleInput` | Cloned action asset per slot + device filter |

## Unity wiring checklist

Phase 2 code is in place; scenes still need Editor wiring for a playable loop:

1. **Main Menu** — enable **Local Multiplayer** button → wire to `MainMenuController.localMultiplayerButton`
2. **LocalMatchSetup** scene — add UI buttons (2/3/4 players, Back) → `LocalMatchSetupController`
3. **Arena_Industrial_01** — add:
   - `DeathmatchManager` with human/bot prefabs + spawn points
   - `LocalMatchRuntime` with `InputActionAsset` reference
   - `CombatHUDController` with one panel per slot (0–3)
   - Optional `VehicleCameraRig` prefab (camera + Cinemachine)
4. **Build Settings** — `LocalMatchSetup` scene included (already in `EditorBuildSettings`)

## Input

- Slot 0: first gamepad, or keyboard if no gamepad
- Slots 1–3: additional gamepads (`Gamepad.all` order)
- Each human gets a **cloned** `CombatVehicle_P0` action map scoped to their device

## Camera

- `MatchConfig.splitScreen = true` (default for couch) → quarter/half viewports via `SplitScreenLayout`
- Shared-screen FFA: set `splitScreen = false` on couch config (future menu toggle)

## Next phase

**Phase 3 — LAN** (`LanHostSession` / `LanClientSession` + Mirror transport). See [MULTIPLAYER.md](MULTIPLAYER.md).
