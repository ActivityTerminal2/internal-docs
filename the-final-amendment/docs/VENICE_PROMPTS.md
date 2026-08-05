# Venice.ai — 2D Art Prompts

Project Dusk uses **[Venice.ai](https://venice.ai/)** for **all 2D art**. Meshy.ai is for 3D only — see [MESHY_PROMPTS.md](MESHY_PROMPTS.md).

---

## Style Primer (paste first in every Venice session)

Copy this block before your asset-specific prompts so every generation stays on-brand:

> You are generating 2D art for **Project Dusk**, a dark industrial vehicular combat game inspired by **Twisted Metal Black** and **late-PS2 / early-2000s arcade UI**. The look is **gritty, chunky, and readable at small sizes** — not modern, not photorealistic, not glossy UI design. Think rusted factory yards, smog, sodium-orange floodlights, toxic green glow, and welded scrap-metal vehicles. Mood is **hostile and industrial**, with occasional dark humor (armored ice-cream truck energy), but never cartoon-cute or sci-fi clean.
>
> All assets should feel like they belong on a **PS2-era game HUD or menu**: **flat or lightly shaded 2D sprites**, **bold silhouettes**, **minimal fine detail**, and **simple color blocking**. Avoid soft gradients, lens flare, bloom, 4K texture noise, realistic lighting, and modern mobile-game UI gloss. Surfaces are **scratched metal, rust, soot, hazard paint, and grime** — not polished chrome or neon cyberpunk. Shapes should stay **legible at 128×128 and below** for icons, and **clear at a glance** for HUD bars and weapon symbols.
>
> **Color palette (stick to these):** soot black `#1a1208` (backgrounds/HUD bases), rust `#8b4513` (borders/accents), toxic green `#3d5c2e` (energy/highlights), amber `#d4a017` (weapons/warnings), industrial orange `#c45c20` (sodium lights). Use **transparent backgrounds** for HUD icons, bars, frames, and VFX sprites; use **dark/black backgrounds** for full-screen UI art unless transparency is requested. **No text in the image** unless the prompt explicitly asks for a blank lettering plate (e.g. winner banner with an empty text area).
>
> Match the **same illustration style** across every asset: same line weight, same level of detail, same flat-shaded industrial tone, same palette discipline. Vehicle portraits, HUD frames, weapon icons, and profile avatars should look like they came from **one art pass on the same game**, not separate art styles. When in doubt, prioritize **clarity, contrast, and chunky retro readability** over decoration.

---

## Workflow

1. **Paste** the Style Primer above into Venice.ai.
2. **Generate** PNG at the exact pixel size listed below (prefer transparent alpha for HUD/icons).
3. **Import** to `Assets/_ProjectDusk/Art/2D/` — Texture Type: **Sprite (2D and UI)**.
4. **Filter:** Point for pixel-crisp HUD; Bilinear for large backgrounds.
5. **Assign** to uGUI `Image` or `SpriteRenderer` billboards.
6. **Metadata** — add `VeniceAssetMetadata` component (prompt, date, style notes).
7. **Copy branding** — logo files also live in `docs/assets/` for README.

---

## Prompt Formula

```
[Asset type] + PS2-era vehicular combat game UI + Twisted Metal Black dark industrial mood + rust metal and toxic green accents + chunky low-detail + flat game sprite + transparent or black background + [WIDTH]x[HEIGHT] pixels
```

### Palette Reference

| Name | Hex | Use |
|------|-----|-----|
| Soot black | `#1a1208` | Backgrounds, HUD base |
| Rust | `#8b4513` | Typography accents, borders |
| Toxic green | `#3d5c2e` | Highlights, energy UI |
| Amber | `#d4a017` | Weapon icons, warnings |
| Industrial orange | `#c45c20` | Sodium light accents |

---

## Phase 1 Asset List (with sizes)

### Branding

| Asset | Size (W×H) | Alpha | Import path |
|-------|------------|-------|-------------|
| Logo banner | **1200×400** | No (black bg) | `docs/assets/logo.png` + `Art/Branding/logo.png` |
| Logo icon | **512×512** | No (dark bg) | `docs/assets/logo-icon.png` + `Art/Branding/logo-icon.png` |
| Boot splash logo | **1024×512** | Yes (transparent) | `Art/2D/UI/bootup/boot.png` |

### UI — Menus & flow

| Asset | Size (W×H) | Alpha | Import path |
|-------|------------|-------|-------------|
| Main menu background | **1920×1080** | No | `Art/2D/UI/main-menu-bg.png` |
| Vehicle select card frame | **512×512** | Yes | `Art/2D/UI/vehicle-card-frame.png` |
| Match-end winner banner | **1024×256** | Yes | `Art/2D/UI/winner-banner.png` |
| Menu button frame (optional) | **320×64** | Yes | `Art/2D/UI/button-frame.png` |

### UI — Vehicle portraits

| Asset | Size (W×H) | Alpha | Import path |
|-------|------------|-------|-------------|
| Rustbucket portrait | **512×512** | Yes | `Art/2D/Vehicles/rustbucket.png` |
| Creepsicle portrait | **512×512** | Yes | `Art/2D/Vehicles/creepsicle.png` |
| Riveter portrait | **512×512** | Yes | `Art/2D/Vehicles/riveter.png` |

### HUD — Bar frames

| Asset | Size (W×H) | Alpha | Import path |
|-------|------------|-------|-------------|
| Health bar frame | **256×32** | Yes | `Art/2D/HUD/health-bar-frame.png` |
| Energy bar frame | **256×32** | Yes | `Art/2D/HUD/energy-bar-frame.png` |
| Turbo / nitro bar frame | **256×32** | Yes | `Art/2D/HUD/turbo-bar-frame.png` |
| MG heat bar frame (optional) | **256×32** | Yes | `Art/2D/HUD/mg-heat-bar-frame.png` |

### HUD — Icons & indicators

| Asset | Size (W×H) | Alpha | Import path |
|-------|------------|-------|-------------|
| Machine gun heat lamp | **64×64** | Yes | `Art/2D/HUD/mg-heat-light.png` |
| Homing weapon icon | **128×128** | Yes | `Art/2D/HUD/weapons/homing.png` |
| Fire weapon icon | **128×128** | Yes | `Art/2D/HUD/weapons/fire.png` |
| Power weapon icon | **128×128** | Yes | `Art/2D/HUD/weapons/power.png` |
| Special weapon icon | **128×128** | Yes | `Art/2D/HUD/weapons/special.png` |

### Profile

| Asset | Size (W×H) | Alpha | Count | Import path |
|-------|------------|-------|-------|-------------|
| Avatar preset | **256×256** | No (dark bg) | **12** | `Art/2D/Profile/avatars/avatar_01.png` … `avatar_12.png` |
| Profile banner | **1024×256** | No | **6** | `Art/2D/Profile/banners/banner_01.png` … `banner_06.png` |

### VFX billboards

| Asset | Size (W×H) | Alpha | Import path |
|-------|------------|-------|-------------|
| Muzzle flash | **128×128** | Yes | `Art/2D/VFX/muzzle-flash.png` |
| Explosion | **128×128** | Yes | `Art/2D/VFX/explosion.png` |
| Smoke puff (optional) | **128×128** | Yes | `Art/2D/VFX/smoke-puff.png` |
| Turbo trail (optional) | **64×64** | Yes | `Art/2D/VFX/turbo-trail.png` |

### Phase 1 totals

| Category | Assets | Notes |
|----------|--------|-------|
| Branding | 3 | Boot logo used by `ActivityTerminal2BootSequence` |
| Menus | 3–4 | Background is full HD; frames are square/wide UI |
| Vehicle portraits | 3 | One per playable rig |
| HUD bars | 3–4 | All **256×32** — same height, swap fill color in code |
| HUD icons | 5 | 4 weapons + MG heat lamp |
| Profile | 18 | 12 avatars + 6 banners |
| VFX | 2–4 | Billboard sprites over 3D |
| **Total (core)** | **37–39** PNG files | Excludes optional items |

---

## Ready-to-Use Prompts

Each prompt assumes you already pasted the **Style Primer**. Include the listed size in your Venice request.

### Logo Banner — 1200×400

> Project Dusk game logo, wide banner, 1200x400 pixels, dark industrial vehicular combat, PS2-era title screen, rust metal typography, toxic green accent, Twisted Metal inspired mood, flat 2D game branding, isolated on black background

### Logo Icon — 512×512

> Project Dusk game logo icon, square 512x512 pixels, blocky PS2-era title screen branding, rust and toxic green, minimal retro game typography, flat 2D app icon, isolated on dark background

### Boot Splash Logo — 1024×512

> ActivityTerminal 2 boot splash logo, PS2 startup screen style, 1024x512 pixels, dark industrial system boot branding, rust metal plate, toxic green accent line, flat 2D game logo, transparent background

### Main Menu Background — 1920×1080

> PS2-era vehicular combat game main menu background, 1920x1080 pixels, dark industrial factory interior, rust pipes, smog, sodium orange lights, widescreen 16:9, no text, game UI backdrop

### Vehicle Select Card Frame — 512×512

> PS2 vehicular combat vehicle select card frame, 512x512 pixels, dark metal border, rust rivets, toxic green corner accents, empty center for vehicle portrait, flat 2D UI sprite, transparent background

### Vehicle Portrait — Rustbucket — 512×512

> PS2 vehicular combat vehicle portrait card, 512x512 pixels, rusty muscle car with weapon pods, dark industrial, front three-quarter view, flat illustration, game vehicle select UI, transparent background

### Vehicle Portrait — Creepsicle — 512×512

> PS2 vehicular combat vehicle portrait card, 512x512 pixels, armored ice cream truck with roof turret, dark humor, rust and graffiti, front three-quarter view, flat illustration, game vehicle select UI, transparent background

### Vehicle Portrait — Riveter — 512×512

> PS2 vehicular combat vehicle portrait card, 512x512 pixels, compact welded armor combat car, rivets and mine dispenser, grey rust metal, front three-quarter view, flat illustration, game vehicle select UI, transparent background

### HUD Health Bar Frame — 256×32

> PS2 Twisted Metal Black HUD health bar frame, 256x32 pixels, horizontal, dark metal border, rust and red accent, chunky low-detail, flat 2D sprite, transparent background

### HUD Energy Bar Frame — 256×32

> PS2 vehicular combat HUD energy bar frame, 256x32 pixels, horizontal, toxic green accent glow, dark industrial metal border, flat 2D sprite, transparent background

### Turbo / Nitro Bar Frame — 256×32

> PS2 vehicular combat HUD turbo nitro bar frame, 256x32 pixels, horizontal, amber glow border, dark metal, flat 2D sprite, transparent background

### Machine Gun Heat Indicator — 64×64

> PS2 Twisted Metal Black HUD indicator, 64x64 pixels, machine gun overheat warning light, small circular lamp, red glow when hot, amber when cool, flat 2D sprite, transparent background

### HUD Homing Weapon Icon — 128×128

> PS2 game HUD icon, 128x128 pixels, homing missile symbol, chunky style, amber on dark, flat 2D sprite, transparent background, Twisted Metal Black weapon display

### HUD Fire Weapon Icon — 128×128

> PS2 game HUD icon, 128x128 pixels, fire missile symbol, flame shape, chunky style, orange and amber, flat 2D sprite, transparent background

### HUD Power Weapon Icon — 128×128

> PS2 game HUD icon, 128x128 pixels, power missile symbol, lightning bolt shape, chunky style, toxic green accent, flat 2D sprite, transparent background

### HUD Special Weapon Icon — 128×128

> PS2 game HUD icon, 128x128 pixels, special weapon star symbol, chunky style, rust red accent, flat 2D sprite, transparent background

### Winner Banner — 1024×256

> PS2 arena combat match winner banner, 1024x256 pixels, wide horizontal, rust metal plate, empty toxic green text plate area, no words, dark industrial, flat 2D UI sprite, transparent edges

### Profile Avatar Preset — 256×256 (×12 variants)

> PS2 vehicular combat player avatar icon, 256x256 pixels, industrial helmet silhouette, toxic green accent, chunky flat portrait, game profile icon, dark background

Generate **12 variants** with different helmet/vehicle silhouettes. Save as `avatar_01.png` … `avatar_12.png`.

### Profile Banner Preset — 1024×256 (×6 variants)

> PS2 game player profile banner, 1024x256 pixels, wide industrial factory skyline, rust and smog, toxic green accent stripe, no text, flat illustration

Generate **6 variants** with different skyline/sky tones. Save as `banner_01.png` … `banner_06.png`.

### Muzzle Flash Billboard — 128×128

> PS2 game muzzle flash sprite, 128x128 pixels, orange yellow burst, low detail flat billboard, transparent background, vehicular combat weapon effect

### Explosion Billboard — 128×128

> PS2 game explosion sprite, 128x128 pixels, fire and smoke blob, low detail flat billboard, orange and black, transparent background

---

## Style Consistency Rules

1. **One palette** across all Venice assets — reference table above.
2. **Exact export sizes** — generate at the listed dimensions; do not upscale small icons.
3. **Chunky silhouettes** — readable at 128×128 and below.
4. **No photorealism** — flat shading, minimal gradients.
5. **Reuse portrait style** for HUD weapon icons and profile avatars.
6. Document each prompt in `VeniceAssetMetadata` for regeneration.

---

## README & Website Reuse

| Asset | Size | Also used in |
|-------|------|--------------|
| `docs/assets/logo.png` | 1200×400 | README header, website home, in-game Main Menu |
| `docs/assets/logo-icon.png` | 512×512 | Favicon, Steam capsule stub, app icon |
| Menu background crops | 1920×1080 | Website hero sections |
| Avatar presets | 256×256 | Website Gravatar fallback — see [WEBSITE.md](WEBSITE.md) |

---

## Related Documents

- [MESHY_PROMPTS.md](MESHY_PROMPTS.md) — 3D assets
- [WEBSITE.md](WEBSITE.md) — web theme and Gravatar fallback sprites
- [ENHANCED_GS_RENDERING.md](ENHANCED_GS_RENDERING.md) — HUD renders sharp over CRT
- [AI_CODED.md](../AI_CODED.md) — Venice.ai disclosure
