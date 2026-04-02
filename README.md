# Mollie Hamman — Personal Website

## Design Choices

### Aesthetic: Retrowave / Synthwave
The site uses a **retrowave** (also called synthwave) aesthetic — inspired by 1980s neon
culture, arcade games, and sci-fi. Think: glowing pinks, electric purples, neon cyan, and
a deep dark background. This style is classic yet bold, and gives the site a memorable
personality that stands out from the typical clean-white portfolio.

The perspective grid in the hero section is a signature retrowave element, evoking the
look of classic video games and 80s movie intros.

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
Three fonts work together:

- **Press Start 2P** — pixel font for the logo and year labels. Maximum retro energy.
- **Orbitron** — futuristic geometric font for section headings and the name. Wide
  letter-spacing makes it feel like a sci-fi interface.
- **Space Mono** — monospace font for body text. Keeps the techy, terminal vibe while
  still being readable.

All three fonts are loaded from Google Fonts (free, no account needed).

### Layout
The page is broken into clear sections, each on its own "screen":

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

## How to Customize

### Update Your Bio
Open `index.html` and look for the comments marked `<!-- ✏️  Edit ... -->`. Those mark
every section you should personalize.

### Add More Gallery Images
1. Drop the image file into the `marketing pictures/` folder.
2. In `index.html`, copy one of the existing `<div class="gallery-card">` blocks and
   update the `src`, `alt`, and caption text.

### Add More Timeline Entries
In `index.html`, find the `<div class="timeline">` section and copy one
`<div class="timeline-item">` block. Update the year, title, and description.

### Change the Color Theme
All colors are defined as CSS custom properties at the top of `style.css` inside `:root`.
Change any hex value there and it will update everywhere on the site.

### Add Social Links
In the footer of `index.html`, replace the `href="#"` placeholders with your real URLs.

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

## To Open the Site
Just double-click `index.html` — it will open in your browser. No server needed.
If you want to share it online, you can host it for free on **GitHub Pages** or **Netlify**.
