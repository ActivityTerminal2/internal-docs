# CLI Launch Flags

Project Dusk parses command-line arguments at startup in the **Bootstrap** scene via `LaunchArgsParser` → `LaunchConfig` singleton. Settings from `settings.json` load first; CLI flags override for that session.

---

## Usage

```bash
# Windows
ProjectDusk.exe --quality=high --crt=medium --fps=60

# Linux
./ProjectDusk.x86_64 --windowed --width=1280 --height=720

# Unity Editor (Play mode)
# Edit → Project Settings → Player → Resolution and Presentation
# Or pass via IDE run configuration / custom batch file
```

Arguments are case-insensitive. Boolean flags without `=value` are treated as `true`.

---

## Display

| Flag | Type | Default | Effect |
|------|------|---------|--------|
| `--width=<int>` | int | From settings | Window width in pixels |
| `--height=<int>` | int | From settings | Window height in pixels |
| `--800x600` | preset | — | Shorthand for `--width=800 --height=600` |
| `--fullscreen` | bool | From settings | Exclusive/fullscreen mode |
| `--windowed` | bool | — | Force windowed mode |

---

## Graphics & Enhanced GS

| Flag | Type | Default | Effect |
|------|------|---------|--------|
| `--quality=low\|medium\|high` | enum | `medium` | Enhanced GS enhancement tier via `PS2RenderProfile` |
| `--fps=<int>` | int | `60` | Target frame rate (`Application.targetFrameRate`) |
| `--no-crt` | bool | off | Disable CRT post-process filter entirely |
| `--crt=low\|medium\|high` | enum | From settings | CRT filter preset strength |
| `--crt-strength=<0.0-1.0>` | float | `0.6` | Fine-grained CRT intensity override |

Quality tiers map to [ENHANCED_GS_RENDERING.md](ENHANCED_GS_RENDERING.md) Low / Medium / High tables.

---

## Audio

| Flag | Type | Default | Effect |
|------|------|---------|--------|
| `--nosound` | bool | off | Mute all audio output |
| `--nomusic` | bool | off | Mute Music mixer group |
| `--novoice` | bool | off | Mute Voice mixer group (future voice lines) |

---

## UI & Gameplay

| Flag | Type | Default | Effect |
|------|------|---------|--------|
| `--nohud` | bool | off | Disable combat HUD canvas |
| `--noboot` | bool | off | Skip ActivityTerminal 2 boot splash |
| `--language=<code>` | string | `en` | Locale stub (string table; Phase 1: English only) |
| `--subtitles=on\|off` | enum | From settings | Subtitle preference (future voice vignettes) |

---

## Save System (Development)

| Flag | Type | Default | Effect |
|------|------|---------|--------|
| `--save-unencrypted` | bool | off | Read/write plain JSON saves instead of encrypted `.pdusk` |

**Not for release builds.** Disabled when `SAVE_ENCRYPTION_REQUIRED` scripting define is set.

---

## Networking (Development Stubs)

Phase 1 flags are parsed and logged; session implementations activate in later phases.

| Flag | Type | Default | Effect |
|------|------|---------|--------|
| `--host-lan` | bool | off | Start as LAN host on default port **7777** (Phase 3) |
| `--join=<ip:port>` | string | — | Join LAN game at address, e.g. `--join=192.168.1.10:7777` (Phase 3) |
| `--dedicated-server` | bool | off | Run headless authoritative server (Phase 4) |
| `--connect=<host:port>` | string | — | Join online server by hostname or IP (Phase 4) |
| `--port=<int>` | int | `7777` | Listen/connect port override |
| `--max-players=<int>` | int | `4` | Max combatants (dedicated server) |
| `--bots=<int>` | int | auto | Bot count fill (dedicated server) |
| `--arena=<id>` | string | `Industrial_01` | Arena definition id (dedicated server) |

### Examples

```bash
# Phase 3 — LAN host (future)
ProjectDusk.exe --host-lan --quality=medium

# Phase 3 — LAN client (future)
ProjectDusk.exe --join=192.168.1.42:7777

# Phase 4 — dedicated server (future)
ProjectDuskServer.x86_64 --dedicated-server --port=7777 --arena=Industrial_01 --bots=2

# Phase 4 — internet client (future)
ProjectDusk.exe --connect=example.com:7777
```

---

## Flag Precedence

1. **Built-in defaults** (code)
2. **`settings.json`** (persisted user preferences)
3. **CLI flags** (highest — override for current session only)

Settings changed in-game write to `settings.json` but do not retroactively alter CLI for the current run.

---

## LaunchConfig Singleton

Parsed flags are exposed on `LaunchConfig.Instance`:

```csharp
public sealed class LaunchConfig
{
    public static LaunchConfig Instance { get; }

    public int TargetFrameRate { get; }
    public GraphicsQualityTier QualityTier { get; }
    public bool NoHud { get; }
    public bool NoSound { get; }
    public bool NoCrt { get; }
    public CrtPreset CrtPreset { get; }
    public bool SaveUnencrypted { get; }
    public NetworkLaunchMode NetworkMode { get; }  // stub
    public string JoinEndpoint { get; }
    // ...
}
```

`GameBootstrap` applies `LaunchConfig` before loading MainMenu.

---

## Related Documents

- [ARCHITECTURE.md](ARCHITECTURE.md) — bootstrap flow
- [ENHANCED_GS_RENDERING.md](ENHANCED_GS_RENDERING.md) — quality tiers
- [SAVE_FORMAT.md](SAVE_FORMAT.md) — `--save-unencrypted`
- [MULTIPLAYER.md](MULTIPLAYER.md) — networking flags
- [BUILD.md](BUILD.md) — building executables
