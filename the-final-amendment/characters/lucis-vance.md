# Lucis Vance

**Arena name:** Glitch  
**Vehicle:** Tick (1994 Krane industrial crane truck / magnet trapper)  
**Portrait asset:** `Marcus.png` (legacy filename — consider renaming to `Glitch.png` / `Lucis.png` later)  
**Status:** Canon — matches runtime `driverRealName` on Tick

> Private lore. Do not ship in public READMEs. Lives in [internal-docs](https://github.com/ActivityTerminal2/internal-docs).

**Name note:** **Lucis Vance** is Glitch’s civilian identity. Do not confuse with **Marcus Thorne** (Grave), **Silus Vane** (world leader), or the retired draft name “Marcus Vance.”

---

## Snapshot

| Field | Value |
|-------|--------|
| Full name | Lucis Vance |
| Arena handle | Glitch |
| Role in roster | Disruption / trapper; antagonist-adjacent combatant |
| Occupation (before) | Tow truck operator |
| Affiliation | Early volunteer for Silus Vane’s games |
| Tone | Split self — quiet civilian vs predatory alter |

---

## Biography

Lucis Vance struggled with violent impulses from childhood. Tow work gave him structure: stranded motorists, clear jobs, a life that looked normal. Therapy and medication kept the darker thoughts manageable for years.

In the week of **August 12, 1997**, a new prescription shifted the balance. Aggression rose; inhibitions fell. **Glitch** surfaced as intrusive thoughts, then a voice, then a second will Lucis could not hold down.

On **August 16, 1997**, Glitch took full control. Lucis woke later with no memory of the Interstate 445 massacre — only sirens, wreckage, and blood. When arrested, Glitch spoke through him, laughing about the carnage.

Prison suited Glitch. He became an enforcer. When Silus Vane opened the arenas, Glitch volunteered early. **Tick** was built to his appetite: the magnet as how he pulls victims in; the electrical overload as how he overran Lucis’s mind.

Lucis is still in there, sometimes. Glitch does not care.

---

## Ties to other cast

| Character | Link |
|-----------|------|
| **Grave** (Marcus Thorne) | Survivor of the I-445 massacre. Entered the games to hunt Glitch / the body of Lucis Vance. |
| **Silus Vane** | Host who welcomed Glitch as volunteer spectacle. |
| **Jinx / Warden** | Fellow contestants; no special allegiance. |

---

## Vehicle symbolism (Tick)

- **Magnet / crane** — Glitch draws others into his orbit; Lucis loses agency.
- **Electrical overload special** — the seizure of one mind by another.
- **Tow-truck / crane chassis** — Lucis’s old life, weaponized.
- **Handprint scratches on the arm** — “collections”; trophies Glitch keeps.

---

## Voice / writing notes

- **Lucis:** quiet, ashamed, incomplete sentences when he surfaces.
- **Glitch:** cruel humor, boasts, treats Lucis as a broken tool.
- Avoid making Glitch “cool”; he is the massacre, not a tragic antihero. Lucis is the tragedy.
- Keep UI/story labels: arena name **Glitch**, legal name **Lucis Vance**.

---

## Open design questions

- [ ] How often Lucis surfaces in story mode (if at all)
- [ ] Rename portrait asset from `Marcus.png` to match Lucis/Glitch
- [ ] Whether Grave’s confrontation can reach Lucis underneath Glitch

---

## Implementation checklist

- [x] Runtime Tick `driverRealName` = Lucis Vance / `driverName` = Glitch
- [ ] Align portrait/VO filenames with Lucis/Glitch
- [ ] Story mode: Grave vs Glitch beat; optional Lucis flicker
- [ ] Promote VO/art via `internal-assests` → `public-assests` when that chapter ships

---

## Related docs

- [Marcus Thorne / Grave](marcus-thorne.md)
- [Anya Petrova / Jinx](anya-petrova.md)
- [Silas Croft / Warden](silas-croft.md)
- [Silus Vane](silus-vane.md)
- [Back story dump](../back-story.txt)
