# Project Dusk — Roadmap

This roadmap tracks where **Project Dusk** is today and where it's headed. It is a living
document — dates are intentionally omitted; items ship when they're ready. Status keys:

- ✅ **Done** — implemented and in the current build
- 🚧 **In progress** — actively being built
- 🗓️ **Planned** — designed / scaffolded, not yet built
- 💡 **Idea** — under consideration, not committed

> **AI disclosure:** Project Dusk is 100% AI-coded. See [AI_CODED.md](AI_CODED.md).

---

## Phase 1 — Offline Deathmatch (current)

The core single-player-vs-bots experience.


| Status | Item                                                                                     |
| ------ | ---------------------------------------------------------------------------------------- |
| ✅      | Quick Match: 1 human vs 3 bots, last vehicle standing                                    |
| ✅      | 4 combat vehicles — Rustbucket, Creepsicle, Riveter, Tick                                |
| ✅      | Per-car specials — homing barrage, tracking flamethrower, radial engines, magnetic crane |
| ✅      | Weapon sandbox — machine gun, homing / fire / freeze / power missiles, mines             |
| ✅      | Finite ammo + weapon pods that respawn over time                                         |
| ✅      | Energy, overdrive, shields, and ram mechanics                                            |
| ✅      | Bot AI — targeting, weapon use, mine-laying, pickup seeking                              |
| ✅      | Enhanced GS rendering (PS2-style) with CRT filter and quality tiers                      |
| ✅      | Driver backstories with narration audio                                                  |
| ✅      | Animated main menu showcase (cars drive, aim, and attack in a black void)                |
| ✅      | Menu + match music with backstory ducking                                                |
| ✅      | Encrypted `.pdusk` saves and CLI launch flags                                            |
| 🗓️    | Additional arenas beyond Industrial 01                                                   |
|        |                                                                                          |
|        |                                                                                          |




## Phase 2 — Local Couch Multiplayer

2–4 humans on one machine. Systems are coded; scenes need final wiring.
See [docs/PHASE_2.md](docs/PHASE_2.md).


| 🗓️ | Split-screen layouts for 1–4 players                |     |
| --- | --------------------------------------------------- | --- |
| 🗓️ | Per-slot input device routing                       |     |
| 🗓️ | Local Multiplayer menu enabled and wired end-to-end |     |
| 🗓️ | Shared-screen FFA toggle                            |     |
| 🗓️ | Couch bot-fill balancing                            |     |




## Phase 3 — LAN

Peer-to-peer play on a local network via a Mirror-based transport.
See [docs/MULTIPLAYER.md](docs/MULTIPLAYER.md).


| Status | Item                                                   |
| ------ | ------------------------------------------------------ |
| 🗓️    | `LanHostSession` / `LanClientSession` implementations  |
| 🗓️    | Mirror transport integration behind session interfaces |
| 🗓️    | Host/join by local IP UI                               |




## Phase 4 — Dedicated Server & Online (Unranked)


| Status | Item                                           |
| ------ | ---------------------------------------------- |
| 🗓️    | Headless authoritative `DedicatedServer` build |
| 🗓️    | `OnlineClient` connect by public IP / hostname |
| 🗓️    | Server browser / direct connect UI             |




## Phase 5 — Ranked Online


| Status | Item                                                                            |
| ------ | ------------------------------------------------------------------------------- |
| 🗓️    | Matchmaking into ranked pools                                                   |
| 🗓️    | Online profiles + Gravatar ([docs/ONLINE_PROFILES.md](docs/ONLINE_PROFILES.md)) |
| 🗓️    | Rankings backend + leaderboards website ([docs/WEBSITE.md](docs/WEBSITE.md))    |


---



## Ideas / Backlog

Not committed to any phase yet:

- 💡 More vehicles and driver stories
- 💡 Environmental hazards and destructible arena props
- 💡 Additional game modes (team deathmatch, objective-based)
- 💡 Replay / spectator camera
- 💡 Accessibility options (colorblind palettes, remappable everything, subtitles)
- 💡 Controller rumble and haptics polish

---



## Contributing

Have a suggestion? Open a GitHub issue or discussion. Credits for contributors live in
[CREDITS.md](CREDITS.md). This roadmap reflects direction, not a promise — priorities can
shift as the game evolves.