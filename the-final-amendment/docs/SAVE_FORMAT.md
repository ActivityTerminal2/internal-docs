# Save Format — `.pdusk`

Project Dusk stores gameplay progress in encrypted **`.pdusk`** binary files. Settings remain plain JSON (`settings.json`) for easy editing.

---

## Overview

| Property | Value |
|----------|-------|
| Extension | `.pdusk` |
| Location | `Application.persistentDataPath/saves/` |
| Encryption | AES-256-GCM |
| Serialization | JSON (in memory) → encrypt → binary on disk |
| Purpose | Tamper deterrence + integrity (auth tag); **not** anti-cheat |
| Slots | 3 manual + 1 autosave |

---

## File Layout

```
┌──────────────────────────────────────────────────────────────┐
│ Offset │ Size │ Field                                        │
├────────┼──────┼──────────────────────────────────────────────┤
│ 0      │ 4    │ Magic: ASCII "PDUS" (0x50 0x44 0x55 0x53)   │
│ 4      │ 1    │ Format version (currently 0x01)              │
│ 5      │ 1    │ Slot id (0=autosave, 1-3=manual)             │
│ 6      │ 8    │ Unix timestamp (UTC, seconds)                │
│ 14     │ 12   │ Nonce / IV (96-bit for AES-GCM)              │
│ 26     │ N    │ Ciphertext (encrypted JSON payload)          │
│ 26+N   │ 16   │ Authentication tag (128-bit GCM tag)         │
└──────────────────────────────────────────────────────────────┘
```

Total header size before ciphertext: **26 bytes**.

---

## Encryption

### Algorithm

- **Cipher:** AES-256-GCM via .NET `System.Security.Cryptography.AesGcm`
- **Key size:** 256 bits (32 bytes)
- **Nonce:** 96 bits (12 bytes), unique per save write
- **Tag:** 128 bits (16 bytes), appended after ciphertext

### Key Derivation

```
key = PBKDF2-HMAC-SHA256(
    password = APP_SECRET + PROJECT_SALT,
    salt     = "project-dusk-save-v1",
    iterations = 100_000,
    keyLength = 32
)
```

| Constant | Location | Notes |
|----------|----------|-------|
| `APP_SECRET` | Embedded in source | Fixed per build; documented as non-secret in open source |
| `PROJECT_SALT` | Embedded in source | `"project-dusk-save-v1"` |
| Machine pepper (optional) | Documented extension | Future: mix `SystemInfo.deviceUniqueIdentifier` hash for per-machine keys |

**Security note:** The key is in the open-source repository by design. Encryption prevents casual file editing and detects corruption — it is **not** a substitute for server-side validation in ranked online play.

---

## Payload Schema (JSON, pre-encryption)

```json
{
  "schemaVersion": 1,
  "savedAtUtc": "2026-07-14T23:00:00Z",
  "slotId": 1,
  "offlineProfile": {
    "displayName": "Player",
    "avatarIconId": "default",
    "bannerId": "default",
    "accentColorId": "rust",
    "favoriteVehicleId": "rustbucket"
  },
  "matchStats": {
    "wins": 0,
    "losses": 0,
    "kills": 0,
    "deaths": 0
  },
  "progression": {
    "lastSelectedVehicleId": "rustbucket",
    "unlockedVehicleIds": ["rustbucket", "creepsicle", "riveter"]
  },
  "settingsSnapshot": {
    "controlScheme": "Classic",
    "graphicsQuality": "Medium"
  },
  "online": null
}
```

### Phase 5 Online Extension

When online accounts are enabled, `online` may contain:

```json
{
  "online": {
    "accountId": "uuid",
    "refreshTokenHash": "sha256...",
    "lastSyncedProfile": { /* OnlinePlayerProfile cache */ },
    "lastSyncUtc": "2026-07-14T23:00:00Z"
  }
}
```

- **No plaintext passwords** stored in saves.
- Refresh token stored as hash only.

---

## Slot Files

| File | Slot ID | Description |
|------|---------|-------------|
| `autosave.pdusk` | 0 | Written on match end / exit (configurable) |
| `slot_1.pdusk` | 1 | Manual save slot 1 |
| `slot_2.pdusk` | 2 | Manual save slot 2 |
| `slot_3.pdusk` | 3 | Manual save slot 3 |

---

## SaveManager API

```csharp
/// <summary>
/// Encrypted save/load for Project Dusk .pdusk files.
/// </summary>
public class SaveManager
{
    bool HasSave(int slotId);
    void Save(int slotId);           // throws SaveException on failure
    SaveData Load(int slotId);       // throws SaveCorruptedException on decrypt/auth failure
    void DeleteSave(int slotId);
}
```

### Error Handling

| Condition | Behavior |
|-----------|----------|
| File missing | `HasSave()` returns false; Load throws `SaveNotFoundException` |
| Wrong magic / version | Load throws `SaveCorruptedException` |
| Auth tag mismatch | Load throws `SaveCorruptedException` — message: *"Save corrupted or tampered"* |
| Truncated file | Load throws `SaveCorruptedException` |

---

## Development Override

| Flag | Effect |
|------|--------|
| `--save-unencrypted` | Write/read plain `.json` files alongside or instead of `.pdusk` |

- Intended for debugging only.
- Release build scripts should define `SAVE_ENCRYPTION_REQUIRED` to disable unencrypted mode in production builds.

Example debug output: `slot_1.json` in the same saves directory.

---

## Platform Paths

| Platform | `persistentDataPath` (typical) |
|----------|-------------------------------|
| Windows | `%USERPROFILE%\AppData\LocalLow\<Company>\<Product>\saves\` |
| Linux | `~/.config/unity3d/<Company>/<Product>/saves/` |
| Steam Deck | Same as Linux — `~/.config/unity3d/...` |

Document exact Company/Product names in build settings when Unity project is created.

---

## Settings (Not Encrypted)

`settings.json` lives alongside saves but is **plain JSON**:

- Display, audio, input, graphics quality, CRT settings
- Low tamper risk; users may edit freely
- CLI flags override at launch; Settings menu writes back to file

---

## Version Migration

When `schemaVersion` increments:

1. `SaveManager` detects version on load.
2. Migration chain runs in memory (v1 → v2 → …).
3. Re-encrypt and write on next save.

Breaking changes bump the binary `format version` byte in the header.

---

## Related Documents

- [ARCHITECTURE.md](ARCHITECTURE.md) — SaveManager in core services
- [CLI_FLAGS.md](CLI_FLAGS.md) — `--save-unencrypted`
- [ONLINE_PROFILES.md](ONLINE_PROFILES.md) — online blob in save
