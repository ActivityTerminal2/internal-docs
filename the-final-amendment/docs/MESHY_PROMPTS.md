# Meshy.ai — 3D Asset Prompts

Project Dusk uses **[Meshy.ai](https://www.meshy.ai/)** for **3D meshes and AI texturing only**. Flat 2D art (logos, HUD, UI) uses [Venice.ai](VENICE_PROMPTS.md).

---

## Workflow

1. **Generate mesh** — one object per generation; isolated on grey background.
2. **AI Texturing pass** — apply texture keywords below.
3. **Export** — FBX or GLB + diffuse textures (prefer CC0/community license when possible).
4. **Import** — `Assets/_ProjectDusk/Art/Models/`
5. **Import preset** — assign `PS2/Lit` (or `PS2/AlphaTest` for cutouts); cap texture size per quality tier.
6. **Metadata** — add `MeshyAssetMetadata` component (prompt, model URL/id, date).

---

## Prompt Formula

```
[Combat vehicle or arena prop] + blocky low-poly + PS2-era vehicular combat game + Twisted Metal Black dark industrial style + [rust/metal] + clean topology + isolated on grey background
```

### Texture Pass Keywords

```
PS2-era vehicular combat texture, rust and scratched metal, hazard stripes, dark industrial, 256x512, minimal PBR, Twisted Metal style
```

---

## Poly Budgets

| Asset Type | Triangle Range |
|------------|----------------|
| Combat vehicle | 5,000 – 15,000 (target 7,000 – 12,000) |
| Arena prop (crate, pipe, wall segment) | 2,000 – 8,000 |
| Pickup prop | 200 – 500 |
| Hero vehicle (High tier showcase) | up to 15,000 |

**Materials:** 1–2 per vehicle; weapon mounts as separate mesh children.

---

## Ready-to-Use Prompts

### Rustbucket — Muscle Car Combat Vehicle

> Blocky low-poly muscle car combat vehicle, PS2 Twisted Metal style, reinforced bumpers, exposed engine, weapon pods on doors, dark red rust metal, 7000-10000 triangles, game vehicle asset, isolated on grey background

**Role:** Balanced starter vehicle. Special: shotgun burst (stub).

---

### Creepsicle — Ice Cream Truck Tank

> Blocky low-poly armored ice cream truck combat vehicle, PS2-era vehicular combat game, dark humor, rust and graffiti, roof-mounted weapon turret stub, 8000-12000 triangles, game-ready, isolated on grey background

**Role:** Heavy tank. Special: toxic spill (stub).

---

### Riveter — Fast Light Car

> Blocky low-poly compact combat car, PS2 Twisted Metal style, welded armor plates, exposed rivets, rear mine dispenser stub, matte grey rust, 6000-9000 triangles, agile game vehicle, isolated on grey background

**Role:** Fast harasser. Special: mine drop (stub).

---

### Industrial Arena Wall Segment

> Blocky low-poly industrial factory wall section, PS2-era arena game prop, rust pipes, warning signs, soot stains, 2000-4000 triangles, modular game environment piece, isolated on grey background

**Use:** Modular arena perimeter — tile and rotate for variety.

---

### Ramp / Jump Piece

> Blocky low-poly metal ramp jump, PS2 arena combat prop, grated steel surface, hazard yellow stripes, welded support beams, 1500-3000 triangles, game environment modular piece, isolated on grey background

---

### Fuel / Health Pickup Crate

> Blocky low-poly military supply crate pickup, PS2 game asset, glowing green health cross or yellow hazard symbol, 500-1500 triangles, game pickup prop, isolated on grey background

---

### Weapon Pickup Pod

> Blocky low-poly floating weapon pickup pod, PS2 vehicular combat game, amber glow, missile silhouette decal, 600-1500 triangles, game pickup prop, isolated on grey background

---

### Explosive Barrel

> Blocky low-poly red explosive barrel, PS2 arena hazard prop, rust and stenciled warning label, 600-1500 triangles, game destructible prop, isolated on grey background should have buttom and top

---

### Toxic Pool Edge Trim

> Blocky low-poly toxic waste pool rim, PS2 arena hazard, green glowing liquid edge, corroded metal lip, 1500-3000 triangles, modular arena piece, isolated on grey background

---

### Exhaust / Smoke Stack (Arena Prop)

> Blocky low-poly factory smokestack section, PS2 industrial arena, soot black metal, riveted seams, 1000-2500 triangles, environment prop, isolated on grey background

---

## Texture Guidelines

| Tier | Max Diffuse Size |
|------|------------------|
| Low | 256 px |
| Medium | 512 px |
| High | 1024 px (hero vehicles); 512 px (props) |

- **No PBR maps** required — diffuse (+ optional simple specular mask) only.
- Palette: rust, soot black, toxic green accents, hazard yellow.
- Avoid photorealistic wear — chunky, readable at PS2 distances.

---

## Import Checklist

- [ ] Scale: 1 unit = 1 meter; vehicle ~4 m long
- [ ] Pivot: ground center for vehicles; base corner for modular walls
- [ ] Normals: consistent outward; no inverted faces
- [ ] UVs: single UV set; minimal stretching on hero faces
- [ ] Shader: `PS2/Lit` assigned via import preset
- [ ] Collider: separate simplified mesh or box collider added in Unity
- [ ] `MeshyAssetMetadata` filled in

---

## What NOT to Generate in Meshy

| Use Venice.ai Instead |
|-----------------------|
| Logo and title art |
| HUD sprites and weapon icons |
| Vehicle select portrait cards |
| Menu backgrounds |
| Profile avatars and banners |

---

## Related Documents

- [VENICE_PROMPTS.md](VENICE_PROMPTS.md) — 2D art prompts
- [ENHANCED_GS_RENDERING.md](ENHANCED_GS_RENDERING.md) — shader and texture tiers
- [ARENAS.md](ARENAS.md) — arena layout using these props
- [AI_CODED.md](../AI_CODED.md) — Meshy.ai disclosure
