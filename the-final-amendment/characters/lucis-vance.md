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

## Character bio audio (transcript)

Canonical VO for the Glitch / Lucis Vance character dossier. Third-person narrator introducing the driver.

> Alright, pull up a chair. You wanted to know about this one. This isn't your usual gangbanger or revolutionary. This one's different. This one's a ghost story.
>
> The name on the birth certificate is Lucis Vance. By all accounts, before 1997, he was a ghost in his own life. Quiet, meticulous tow truck driver. Kept to himself. Neighbors said he was polite, but distant. The kind of guy you'd forget five minutes after you met him. But our shrinks, they dug into his history. Seems Vance spent his whole life looking over his own shoulder. He had... impulses. Dark ones. He built walls around 'em, see? Therapy, pills, a job with rules so tight you couldn't breathe. Helping stranded motorists, that was his penance. Gave him a sense of control, he thought. A dam holding back a tidal wave of ugly.
>
> Then came August '97. The dam broke.
>
> New medication. That's what the file says. Some new wonder drug supposed to smooth him out. Only it did the opposite. It sanded down the walls in his head until there was nothing left. The thing he called 'Glitch'... it wasn't new. It was always there, just locked in a cage. The pills didn't just unlock the door; they tore it off the hinges.
>
> It started slow. Whispers in his head. Then the whispers started talking back. Then, on the 16th of August, Lucis Vance just... clocked out. Went on permanent vacation. Glitch punched the clock and took over the wheel.
>
> The Interstate 445 incident... you've read the reports. But they don't capture the feel of it. The guys on the scene said it wasn't a rage-fueled rampage. It was... efficient. Calculated. When they finally boxed in his truck, he wasn't scared, he wasn't angry. He was just sitting there, smiling. When they pulled him out, he laughed. Said, 'This ain't the end for me. Glitch is here to stay, boys and girls.' Lucis Vance was just along for the ride.
>
> In prison, he was a kingfish in a small pond. A predator in a shark tank. He didn't just survive; he thrived. So when Vane's goons came looking for volunteers for his little death show, Glitch was first in line. It wasn't a punishment to him. It was a promotion.
>
> That crane truck of his... it's a perfect extension of the man. That magnet on the end? That's how he got his hooks into Vance's brain. Snatched him right up. And that special of his, the one that makes the other car's systems go haywire and shoot everything at once before he tosses it away? That's his origin story, playing out over and over. He's not just killing them. He's showing them how he was born.
>
> He knows about the trucker, Grave. He knows their history. He thinks it's funny. He's hoping to draw him in the final round. Doesn't want to just kill him. He wants to make Grave watch while he reenacts the day his family died, just for kicks.
>
> There's no getting Lucis back. He's gone. This thing wearing his skin, this Glitch... it's all that's left. And in The Final Amendment, it's found its true calling. It's not a man in a machine. It's a monster that finally found the right skin to wear.

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
