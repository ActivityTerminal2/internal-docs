# Rankings Website

Phase 5 **Project Dusk** leaderboard and profile site — themed to match the game's dark industrial aesthetic and **Enhanced GS Rendering Engine** branding.

Phase 1 stub: `website/README.md` + `website/public/placeholder.html` + this design spec.

---

## Stack (Recommended)

| Layer | Choice | License |
|-------|--------|---------|
| Framework | [Astro](https://astro.build/) or Next.js | MIT |
| Styling | CSS custom properties (design tokens) | — |
| API client | Fetch `services/rankings-api` REST | — |
| Deploy | Vercel, Cloudflare Pages, or Docker | — |

Static/SSR hybrid — leaderboards and public profiles are SSR or ISR for SEO.

---

## Site Map

| Route | Content |
|-------|---------|
| `/` | Logo, tagline, download links, featured top players |
| `/leaderboards` | Sortable tables — rank, avatar, player, W/L, K/D, tier; season selector |
| `/player/{id}` | Public profile — avatar, banner, title, stats, recent matches |
| `/login` | Account management |
| `/register` | Create account (email used for Gravatar when enabled) |
| `/seasons` | Season history and rules |
| `/about` | MIT license, AI disclosure, TM Black–inspired disclaimer |

---

## Design Tokens

Shared with in-game UI (Venice.ai palette):

```css
:root {
  /* Backgrounds */
  --color-bg-soot:        #1a1208;
  --color-bg-panel:       #2a2218;
  --color-bg-panel-hover: #3a3228;

  /* Accents */
  --color-accent-toxic:   #3d5c2e;
  --color-accent-rust:    #8b4513;
  --color-accent-amber:   #d4a017;
  --color-accent-orange:  #c45c20;
  --color-accent-danger:  #8b2020;

  /* Text */
  --color-text-primary:   #e8e0d0;
  --color-text-muted:     #9a9080;
  --color-text-toxic:     #6abf4b;

  /* Borders */
  --color-border-rust:    #5c3a1e;
  --color-border-subtle:  #3a3228;

  /* Typography */
  --font-display:         "Segoe UI", "Helvetica Neue", Arial, sans-serif;
  --font-body:            "Segoe UI", system-ui, sans-serif;
  --font-mono:            "Consolas", "Courier New", monospace;

  /* Spacing */
  --space-xs:  4px;
  --space-sm:  8px;
  --space-md:  16px;
  --space-lg:  24px;
  --space-xl:  48px;

  /* Effects */
  --crt-scanline-opacity: 0.08;
  --avatar-ring-color:    var(--color-accent-rust);
  --avatar-size-sm:       32px;
  --avatar-size-md:       64px;
  --avatar-size-lg:       128px;
}
```

### Optional CRT CSS (Home / About Only)

Subtle scanline overlay — **not** on data-heavy leaderboard tables (readability):

```css
.crt-overlay {
  pointer-events: none;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0, 0, 0, var(--crt-scanline-opacity)) 2px,
    rgba(0, 0, 0, var(--crt-scanline-opacity)) 4px
  );
}
```

---

## Brand Assets

| Asset | Source | Use |
|-------|--------|-----|
| `docs/assets/logo.png` | Venice.ai | Header, favicon source |
| `docs/assets/logo-icon.png` | Venice.ai | Favicon, OG image |
| Main menu background crop | Venice.ai | Hero section background |
| Avatar presets | `Art/2D/Profile/avatars/` | Gravatar fallback |
| Profile banners | `Art/2D/Profile/banners/` | Player profile headers |

Copy Venice assets to `website/public/assets/` at build time or symlink from repo.

---

## Gravatar Integration

### Avatar Component

`Avatar.tsx` (React) or `Avatar.astro` (Astro):

```typescript
interface AvatarProps {
  avatarUrl: string;       // from API — never build from email client-side
  avatarIconId: string;    // preset fallback id
  avatarSource: 'Preset' | 'Gravatar';
  size: 'sm' | 'md' | 'lg';
  displayName: string;   // alt text
}
```

### Render Logic

```
1. Render <img src={avatarUrl} /> from API response
2. onError → fallback to /assets/avatars/{avatarIconId}.png
3. Wrap in .avatar-ring (rust border) for leaderboard thumbnails
```

### Profile Settings Page

- Radio: **Avatar: Preset / Gravatar**
- Preset: grid preview of Venice avatar pack
- Gravatar: preview via authenticated `GET /api/v1/profile/me/avatar-preview`
- Saving PATCHes `/api/v1/profile/me` with `avatarSource`, `useGravatar`, `avatarIconId`

### CSP / img-src

Content-Security-Policy must allow:

```
img-src 'self' https://www.gravatar.com https://cdn.projectdusk.example data:;
```

---

## Leaderboard Table

| Column | Content |
|--------|---------|
| Rank | `#1`, `#2`, … |
| Avatar | `<Avatar size="sm" />` |
| Player | Link to `/player/{id}` — displayName |
| Tier | Badge — Bronze / Gold / etc. |
| W/L | Wins / Losses |
| K/D | Ratio formatted `1.42` |
| ELO | Numeric (optional column) |

Season selector dropdown → `GET /api/v1/leaderboards?season=2026-s1&limit=100`

Arena tabs: Global | Industrial_01 | Industrial_02

---

## Public Profile Page

```
┌─────────────────────────────────────────────────┐
│  [ Banner image — preset id ]                   │
│  ┌──────┐  DisplayName                          │
│  │Avatar│  Title Tag · Tier Badge               │
│  └──────┘  Favorite vehicle: Rustbucket         │
│            Bio text (80 chars max)              │
├─────────────────────────────────────────────────┤
│  Stats: W/L · K/D · ELO · Avg Placement         │
├─────────────────────────────────────────────────┤
│  Recent Matches (table)                         │
│  date | arena | placement | K/D | link          │
└─────────────────────────────────────────────────┘
```

Data: `GET /api/v1/profile/{id}`

---

## Home Page

- Centered **Project Dusk** logo (`docs/assets/logo.png`)
- Tagline: *Twisted Metal Black–inspired arena vehicular combat*
- **Enhanced GS Rendering Engine** blurb with link to GitHub `docs/ENHANCED_GS_RENDERING.md`
- Download buttons → GitHub Releases (Windows ZIP, Linux tar.gz)
- Top 5 players widget from leaderboards API
- Footer: MIT license, [AI_CODED.md](https://github.com/.../AI_CODED.md) link, TM Black–inspired disclaimer

---

## About Page (Required Disclosures)

1. **MIT License** — link to repo LICENSE
2. **100% AI-coded** — link to AI_CODED.md
3. **Original IP disclaimer** — inspired by Twisted Metal Black style; not affiliated with Sony or SingleTrac
4. **Enhanced GS Rendering Engine** — upgraded Graphics Synthesizer for PS2-like games
5. **Meshy.ai / Venice.ai** — asset generation credits

---

## API Integration

```typescript
const API_BASE = import.meta.env.PUBLIC_RANKINGS_API_URL
  ?? 'https://api.projectdusk.example';

async function fetchLeaderboard(season: string, arena?: string) {
  const params = new URLSearchParams({ season, limit: '100' });
  if (arena) params.set('arena', arena);
  const res = await fetch(`${API_BASE}/api/v1/leaderboards?${params}`);
  return res.json();
}
```

Authenticated routes attach `Authorization: Bearer {accessToken}` from httpOnly cookie or secure storage.

---

## Deploy

### Vercel (Example)

```bash
cd website
npm install
npm run build
# Set env: PUBLIC_RANKINGS_API_URL=https://api.projectdusk.example
vercel deploy --prod
```

### Docker (Self-Hosted)

```dockerfile
# website/Dockerfile stub
FROM node:20-alpine AS build
WORKDIR /app
COPY . .
RUN npm ci && npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
```

---

## Phase 1 Stub Files

```
website/
├── README.md              # "Phase 5 — not yet deployed"
├── public/
│   ├── placeholder.html   # Coming soon page with logo + tokens demo
│   └── assets/            # copied Venice branding
├── src/                   # (empty or minimal scaffold)
└── package.json           # (optional stub)
```

---

## In-Game Links

| Menu Entry | Action |
|------------|--------|
| Leaderboards | Opens `{WEBSITE_URL}/leaderboards` in system browser |
| View on Web | Opens `/player/{accountId}` for logged-in user |
| Ranked Online | Requires login → queue (Phase 5) |

Configure `WEBSITE_URL` in game build constants.

---

## Related Documents

- [ONLINE_PROFILES.md](ONLINE_PROFILES.md) — profile fields and API contract
- [VENICE_PROMPTS.md](VENICE_PROMPTS.md) — avatar and banner art
- [ENHANCED_GS_RENDERING.md](ENHANCED_GS_RENDERING.md) — engine branding
- [AI_CODED.md](../AI_CODED.md) — disclosure for About page
