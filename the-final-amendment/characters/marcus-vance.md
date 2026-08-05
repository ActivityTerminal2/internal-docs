# Marcus Vance

**Arena name:** Glitch  
**Vehicle:** Tick (magnetic crane tow truck)  
**Portrait asset:** `Marcus.png`  
**Status:** Canon draft — reconcile runtime `driverRealName` (`Lucis Vance`) to **Marcus Vance**

> Private lore. Do not ship in public READMEs. Lives in [internal-docs](https://github.com/ActivityTerminal2/internal-docs).

---

## Snapshot

| Field | Value |
|-------|--------|
| Full name | Marcus Vance |
| Arena handle | Glitch |
| Role in roster | Antagonist-adjacent combatant; catalyst of the I-445 massacre |
| Occupation (before) | Tow truck operator |
| Affiliation | Silus Vane’s games (volunteer / early entrant) |
| Tone | Split self — methodical civilian vs predatory alter |

Marcus is the man who existed before Glitch. The games know him as Glitch; the files, the portrait folder, and key-member shorthand still say **Marcus**.

---

## Biography

Marcus Vance always carried violent impulses he could not fully name. Tow work gave him structure: stranded motorists, clear jobs, a life that looked normal from the outside. Therapy and medication kept the darker thoughts at bay for years.

In the week of **August 12, 1997**, a new prescription changed the balance. Aggression rose; inhibitions fell. **Glitch** surfaced first as intrusive thoughts, then as a voice, then as a second will Marcus could not hold down.

On **August 16, 1997**, Glitch took full control. Marcus woke later with no memory of the Interstate 445 massacre—only sirens, wreckage, and blood. When arrested, Glitch spoke through him, laughing about the carnage.

Prison suited Glitch. He became an enforcer. When Silus Vane opened the arenas, Glitch volunteered early. The crane truck—**Tick**—was built to his appetite: the magnet as how he pulls victims in; the electrical overload as how he overran Marcus’s mind.

Marcus is still in there, sometimes. Glitch does not care.

---

## Ties to other cast

| Character | Link |
|-----------|------|
| **Grave** (Marcus Thorne) | Victim’s survivor. Grave entered the games to hunt the I-445 killer—Glitch / the body of Marcus Vance. |
| **Silus Vane** | Host of the games; Glitch is a willing spectacle, not a reformer. |
| **Jinx / Warden** | Fellow contestants; no special allegiance. |

**Name note:** Do not confuse **Marcus Vance** (Glitch) with **Marcus Thorne** (Grave). Same given name, different blood and motives.

---

## Vehicle symbolism (Tick)

- **Magnet / crane** — Glitch draws others into his orbit; Marcus loses agency.
- **Electrical overload special** — the seizure of one mind by another.
- **Tow-truck chassis** — Marcus’s old life, weaponized.

---

## Implementation checklist (engine / assets)

- [ ] Set `driverRealName` on Tick / Phase1RuntimeData from `Lucis Vance` → `Marcus Vance`
- [ ] Keep arena name **Glitch**; portrait path `Marcus` / `Marcus.png`
- [ ] Update driver story strings and VO labels to Marcus Vance
- [ ] Promote portrait/VO through `internal-assests` → `public-assests` when the chapter ships
- [ ] Story mode: optional beat where Marcus surfaces briefly under Glitch

---

## Voice / writing notes

- **Marcus:** quiet, ashamed, incomplete sentences when he surfaces.
- **Glitch:** preacher-cruel humor, boasts, treats Marcus as a broken tool.
- Avoid making Glitch “cool”; he is the massacre, not a tragic hero. Marcus is the tragedy.
