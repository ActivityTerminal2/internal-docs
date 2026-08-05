# Build Instructions

Cross-platform IL2CPP builds for **Windows** and **Linux**. Phase 4 adds a headless dedicated server build.

---

## Prerequisites

| Requirement | Notes |
|-------------|-------|
| Unity Hub | [unity.com/download](https://unity.com/download) |
| Unity **6000.3.20f1** LTS | Unity 6.3 with URP |
| Windows Build Support (IL2CPP) | Unity Hub → Add Modules |
| Linux Build Support (IL2CPP) | Cross-compile Linux from Windows |
| Git LFS | `git lfs install` before cloning |

---

## Project Paths

| Output | Path |
|--------|------|
| Windows player | `Builds/Windows/ProjectDusk.exe` |
| Linux player | `Builds/Linux/ProjectDusk.x86_64` |
| Linux server (Phase 4) | `Builds/Server/ProjectDuskServer.x86_64` |

The `Builds/` directory is gitignored. Distribute as portable ZIP folders — no installer.

---

## Build Scripts

### Windows

```powershell
# From repository root
.\tools\build-windows.ps1
```

Invokes Unity in batch mode:

```text
Unity.exe -batchmode -quit -projectPath . -executeMethod ProjectDusk.Build.BuildWindows64
```

Output: `Builds/Windows/ProjectDusk.exe` + `ProjectDusk_Data/`

### Linux (cross-compile from Windows)

```powershell
.\tools\build-linux.ps1
```

Output: `Builds/Linux/ProjectDusk.x86_64` + `ProjectDusk_Data/`

Make executable on Linux:

```bash
chmod +x Builds/Linux/ProjectDusk.x86_64
```

### Dedicated Server (Phase 4 stub)

```bash
./tools/build-server-linux.sh
```

Output: `Builds/Server/ProjectDuskServer.x86_64` — headless, no GPU assets beyond arena data.

---

## Manual Unity Build

1. Open project in Unity 6000.3.20f1 LTS.
2. **File → Build Profiles** (or Build Settings).
3. Scenes in order: Bootstrap → MainMenu → VehicleSelect → Arena_Industrial_01.
4. Platform: **Windows** or **Linux**.
5. Architecture: **x86_64**.
6. Scripting Backend: **IL2CPP**.
7. Development Build: off for release.
8. Build.

---

## Portable Distribution

Zip the entire platform folder:

```powershell
Compress-Archive -Path Builds\Windows\* -DestinationPath ProjectDusk-Windows-x64.zip
```

```bash
cd Builds/Linux && tar -czvf ProjectDusk-Linux-x64.tar.gz .
```

### Saves & Settings Locations

| Platform | Path |
|----------|------|
| Windows | `%USERPROFILE%\AppData\LocalLow\<CompanyName>\<ProductName>\` |
| Linux / Steam Deck | `~/.config/unity3d/<CompanyName>/<ProductName>/` |

Contains `saves/*.pdusk` and `settings.json`. See [SAVE_FORMAT.md](SAVE_FORMAT.md).

---

## Steam Deck / SteamOS

### Display

- Native resolution: **1280×800**
- Default quality: **Medium** Enhanced GS tier
- Test CRT filter at Medium preset for readability on LCD

### Controls

- Default to **gamepad-first** UI focus
- **Steam Menu** button → Pause (Input System binding)
- Verify all three control schemes with Steam Input passthrough disabled (native HID via HIDrogen)

### udev Rules (Controller Permissions)

On Steam Deck desktop mode or generic Linux, ensure user has access to `/dev/input/*` and `/dev/hidraw*`.

Create `/etc/udev/rules.d/99-project-dusk-controllers.rules`:

```udev
# Project Dusk — gamepad access (Steam Deck / Linux)
KERNEL=="js[0-9]*", MODE="0666", GROUP="input"
KERNEL=="hidraw*", MODE="0666", GROUP="input"
SUBSYSTEM=="input", MODE="0666", GROUP="input"
```

Apply rules:

```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

Add your user to the `input` group if needed:

```bash
sudo usermod -aG input $USER
# Log out and back in
```

### Proton vs Native Linux Build

Project Dusk targets a **native Linux IL2CPP** build. On Steam Deck:

1. Add `ProjectDusk.x86_64` as non-Steam game, or
2. Ship via Steam with Linux depot (future)

Proton is not required for the native build.

### Performance Targets

| Setting | Steam Deck Expectation |
|---------|------------------------|
| Quality | Medium |
| FPS | 60 (`--fps=60` default) |
| CRT | Medium preset |
| Resolution | 1280×800 fullscreen |

---

## Windows Firewall (Multiplayer)

When hosting LAN games (Phase 3+), allow inbound UDP/TCP on port **7777**:

```powershell
New-NetFirewallRule -DisplayName "Project Dusk LAN" -Direction Inbound -Protocol UDP -LocalPort 7777 -Action Allow
New-NetFirewallRule -DisplayName "Project Dusk LAN TCP" -Direction Inbound -Protocol TCP -LocalPort 7777 -Action Allow
```

See [MULTIPLAYER.md](MULTIPLAYER.md) for networking details.

---

## Linux Firewall

```bash
# ufw example
sudo ufw allow 7777/udp
sudo ufw allow 7777/tcp
```

For dedicated servers on cloud VPS, open the same port in the provider's security group.

---

## Release Checklist

- [ ] `SAVE_ENCRYPTION_REQUIRED` scripting define enabled
- [ ] `--save-unencrypted` disabled in release
- [ ] Development console disabled
- [ ] Version string updated in Main Menu
- [ ] AI_CODED.md disclosure present in build folder (copy or link from repo)
- [ ] Test Windows x64 clean machine (no Unity installed)
- [ ] Test Linux x64 or Steam Deck
- [ ] Verify gamepad hot-plug after udev rules

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Linux build missing execute bit | `chmod +x ProjectDusk.x86_64` |
| Controller not detected on Linux | Install udev rules; verify HIDrogen package |
| Pink materials | URP asset not included in build — check Graphics settings |
| CRT too dark on Deck | Lower CRT strength in Settings or `--crt=low` |
| Saves not found | Check `persistentDataPath` log line in `Player.log` |

### Log Locations

| Platform | Log |
|----------|-----|
| Windows | `%USERPROFILE%\AppData\LocalLow\<Company>\<Product>\Player.log` |
| Linux | `~/.config/unity3d/<Company>/<Product>/Player.log` |

---

## Related Documents

- [CLI_FLAGS.md](CLI_FLAGS.md) — launch arguments for testing builds
- [MULTIPLAYER.md](MULTIPLAYER.md) — LAN and dedicated server ports
- [ENHANCED_GS_RENDERING.md](ENHANCED_GS_RENDERING.md) — quality tiers
- [CONTROLS.md](CONTROLS.md) — Steam Deck bindings
