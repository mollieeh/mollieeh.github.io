# Mollie Hamman — Personal Website

## Design Choices

### Color Palette
| Name    | Hex       | Used For                        |
|---------|-----------|---------------------------------|
| BG Dark | `#0d0221` | Main background                 |
| Pink    | `#ff006e` | Accents, glitch, timeline dots  |
| Purple  | `#8338ec` | Borders, gradient, glow         |
| Cyan    | `#00f5d4` | Links, highlights, active state |
| Orange  | `#fb5607` | Available for extra accents     |
| Yellow  | `#ffbe0b` | Timeline year labels            |

### Typography

- **Press Start 2P** — pixel font for the logo and year labels.
- **Orbitron** — futuristic geometric font for section headings and the name.
- **Space Mono** — monospace font for body text.

fonts are loaded from Google Fonts

### Layout

1. **Hero** — Full-screen intro with your name and a glitch animation
2. **About** — Two-column layout: bio text on the left, stat cards on the right
3. **Highlights** — A vertical timeline of key life moments
4. **Gallery** — A responsive card grid for your marketing work
5. **Footer** — Contact section with social links

### Responsiveness
The layout is mobile-friendly. The `about-grid` and `gallery-grid` both collapse to a
single column on small screens using CSS Grid's `auto-fit / minmax`.

### Subtle Effects
- **Scanlines overlay** — a repeating horizontal stripe pattern that fakes a CRT monitor
  effect. It's very subtle (8% opacity) and adds texture without being distracting.
- **Glitch animation** — the hero name has a CSS-only glitch effect using `::before` and
  `::after` pseudo-elements with `clip-path` animations.
- **Scroll fade-in** — elements animate in as you scroll down, using the browser's
  `IntersectionObserver` API (no library needed).
- **Lightbox** — clicking a gallery image opens a full-screen viewer with keyboard
  navigation (arrow keys + Escape).

---

## File Structure

```
personal_website/
├── index.html          ← All page content (HTML structure)
├── style.css           ← All visual styling (colors, layout, animations)
├── script.js           ← Interactive behavior (lightbox, scroll animations, nav)
├── README.md           ← This file (design decisions)
├── HELPME.md           ← Coding concepts explained
└── marketing pictures/ ← Your image assets
    ├── WISE_detective_Sept25 copy.png
    ├── WISE_winterWiseWonderland_Dec25 copy.png
    └── hacksmu_registration_announcement copy.png
```