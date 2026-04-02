# HELPME — Coding Concepts Explained

This file explains every major coding concept used in this website,
written so that someone new to web development can understand them.

---

## The Three Languages of the Web

Every website is built with three files that each do one job:

| File        | Language   | Job                                           |
|-------------|------------|-----------------------------------------------|
| `index.html`| HTML       | **Structure** — what's on the page            |
| `style.css` | CSS        | **Appearance** — how it looks                 |
| `script.js` | JavaScript | **Behavior** — what it does when you interact |

Think of it like a house: HTML is the walls and rooms, CSS is the paint and
furniture, and JavaScript is the electricity and plumbing.

---

## HTML Concepts

### Tags and Elements
HTML uses **tags** wrapped in angle brackets. Most tags come in pairs:
```html
<h1>Hello</h1>
```
The opening tag `<h1>` starts the element, and the closing tag `</h1>` ends it.
Everything between them is the content.

Common tags used in this site:
- `<section>` — a large page section
- `<div>` — a generic container (short for "division")
- `<p>` — a paragraph of text
- `<h1>` through `<h3>` — headings (1 is biggest)
- `<a>` — a link (the `href` attribute says where it goes)
- `<img>` — an image (the `src` attribute is the file path)
- `<ul>` / `<li>` — an unordered list and its items
- `<nav>`, `<footer>` — semantic tags that describe the role of the section

### Attributes
Extra information added inside the opening tag:
```html
<img src="photo.png" alt="Description of photo" />
```
- `src` = source (where is the file?)
- `alt` = alternative text (shown if the image fails to load; also used by screen readers)
- `id` = a unique name for that element (used to jump to it with anchor links like `#about`)
- `class` = a reusable label for styling (multiple elements can share a class)

### Semantic HTML
Some tags describe *meaning*, not just appearance:
- `<nav>` — navigation bar
- `<footer>` — bottom of the page
- `<section>` — a thematic grouping of content
- `<h1>` — the main heading (there should only be one per page)

This matters for accessibility (screen readers) and search engines (SEO).

### URL Encoding (`%20`)
File paths in HTML can't have spaces. The space in `marketing pictures/` becomes `%20`:
```html
<img src="marketing%20pictures/photo.png" />
```
`%20` is the "percent-encoded" version of a space character.

### `loading="lazy"`
```html
<img loading="lazy" src="..." />
```
This tells the browser not to load the image until the user is about to scroll to it.
It makes the page load faster because it doesn't download all images up front.

---

## CSS Concepts

### The Cascade
CSS stands for **Cascading Style Sheets**. "Cascading" means rules flow downward — if
two rules target the same element, the one that appears later (or is more specific) wins.

### Selectors
Selectors say *which* HTML elements to style:
```css
p { }            /* all <p> tags */
.card { }        /* any element with class="card" */
#hero { }        /* the element with id="hero" */
.card:hover { }  /* a .card when the mouse is over it */
```

### CSS Custom Properties (Variables)
Defined at the top of `style.css` inside `:root { }`:
```css
:root {
  --pink: #ff006e;
  --cyan: #00f5d4;
}
```
Then used anywhere in the file:
```css
color: var(--pink);
```
Why? Change the value in one place, and it updates everywhere. This is how you'd
change the whole color theme just by editing a few lines.

### The Box Model
Every HTML element is a rectangle. From outside to inside:
1. **Margin** — space outside the element (pushes other things away)
2. **Border** — the visible edge line
3. **Padding** — space inside the element (between content and border)
4. **Content** — the actual text or image

`box-sizing: border-box` (set at the top of the CSS) makes padding and border count
*inside* the element's size, which is far more intuitive.

### CSS Grid
Used for the about section and gallery:
```css
display: grid;
grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
gap: 1.8rem;
```
- `display: grid` turns the container into a grid
- `repeat(auto-fit, minmax(280px, 1fr))` means: "make as many columns as fit,
  each at least 280px wide"
- `1fr` means "one fraction of the available space" — columns grow to fill the row
- `gap` is the space between grid cells

This is how the gallery automatically shows 3 columns on desktop and 1 on mobile —
no JavaScript needed, the browser figures it out.

### Flexbox
Used for the nav, footer links, and stat cards:
```css
display: flex;
align-items: center;
justify-content: space-between;
```
- `display: flex` makes children line up in a row (or column)
- `align-items: center` centers them vertically
- `justify-content: space-between` spreads them to the left and right edges

### Pseudo-elements (`::before`, `::after`)
These let you insert invisible extra elements via CSS, without changing the HTML:
```css
.glitch::before {
  content: attr(data-text);
  color: var(--pink);
}
```
The glitch effect works by drawing the name text twice (slightly offset, in pink and
cyan) on top of the real white text, then clipping and animating them to flicker.

### `clip-path`
Cuts the visible area of an element into a custom shape:
```css
clip-path: inset(0 0 70% 0);
```
`inset(top right bottom left)` clips from each side. Used in the glitch animation to
only reveal a horizontal "slice" of the text at a time.

### CSS Animations (`@keyframes`)
```css
@keyframes glitch-top {
  0%   { clip-path: inset(0 0 100% 0); }  /* fully hidden */
  92%  { clip-path: inset(0 0 70% 0); }   /* partially visible */
  100% { clip-path: inset(0 0 100% 0); }  /* hidden again */
}

.glitch::before {
  animation: glitch-top 3.5s infinite linear;
}
```
`@keyframes` defines the animation steps. `animation` applies it to an element.

### `transition`
A simpler version of animation for hover effects:
```css
transition: transform 0.25s, box-shadow 0.25s;
```
When properties change (like on hover), they smoothly animate over 0.25 seconds
instead of snapping instantly.

### `transform`
Moves or scales elements without changing the page layout:
```css
transform: translateY(-6px);  /* move up 6px */
transform: scale(1.06);       /* zoom in 6% */
```

### CSS Gradients
```css
background: linear-gradient(135deg, var(--cyan), var(--purple));
```
Makes a smooth color transition. `135deg` is the angle (↘ direction).

Radial gradient (circle outward):
```css
background: radial-gradient(circle, rgba(131,56,236,0.18) 0%, transparent 70%);
```

### `rgba()` Colors
`rgba(255, 0, 110, 0.6)` — red, green, blue (0–255), and alpha (0=transparent, 1=opaque).
Lets you use semi-transparent colors for glows and overlays.

### `text-shadow` and `box-shadow`
```css
text-shadow: 0 0 20px rgba(255, 0, 110, 0.6);
```
`x-offset  y-offset  blur-radius  color` — `0 0 20px` makes a centered glow.

### `position: fixed`
The nav bar stays at the top of the screen even when you scroll, because it's
`position: fixed`. `position: absolute` is relative to the nearest positioned ancestor;
`position: relative` is relative to the element's normal spot.

### `z-index`
Controls which element appears on top when they overlap. Higher number = closer to you.
- Nav: `z-index: 100`
- Lightbox: `z-index: 200`
- Scanlines: `z-index: 9999` (always on top of everything)

### `backdrop-filter: blur()`
The nav has a frosted glass effect:
```css
backdrop-filter: blur(10px);
```
Blurs whatever is behind the element. Only works when the element has some transparency.

### `aspect-ratio`
```css
aspect-ratio: 4 / 3;
```
Forces the gallery image containers to always be 4:3 (like an old TV), regardless of
the image's actual dimensions. Keeps cards the same height.

### `object-fit: cover`
```css
object-fit: cover;
```
Makes an image fill its container without stretching, cropping the edges if needed.

### `clamp()`
```css
font-size: clamp(2.5rem, 8vw, 5.5rem);
```
Sets a font size that scales with the viewport but never goes below 2.5rem or above
5.5rem. `vw` = viewport width (1vw = 1% of the screen width).

### `-webkit-background-clip: text`
```css
background: linear-gradient(135deg, var(--pink), var(--cyan));
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```
Makes a gradient *show through the text shape* — so the text appears to be made of the
gradient colors instead of a solid color.

---

## JavaScript Concepts

### `document.querySelectorAll()`
Finds all HTML elements that match a CSS selector and returns a list:
```js
const cards = document.querySelectorAll('.gallery-card');
```

### `addEventListener()`
Listens for an event and runs a function when it happens:
```js
closeBtn.addEventListener('click', closeLightbox);
```
Events: `'click'`, `'keydown'`, `'scroll'`, `'mouseover'`, etc.

### Arrow Functions
A compact way to write functions:
```js
const double = (x) => x * 2;

// Same as:
function double(x) { return x * 2; }
```

### `forEach()`
Loops over every item in an array:
```js
images.forEach((image, index) => {
  console.log(index, image.src);
});
```

### The Modulo Operator (`%`)
Used for wrapping the lightbox index around:
```js
currentIndex = (currentIndex + 1) % images.length;
```
If `images.length` is 3, then after index 2 comes index 0 (wraps back to the start).
`%` gives the *remainder* of division.

### Template Literals
Backtick strings that can embed variables:
```js
const msg = `Image ${currentIndex + 1} of ${images.length}`;
```

### `classList`
Controls an element's CSS classes from JavaScript:
```js
lightbox.classList.add('open');    // adds the class
lightbox.classList.remove('open'); // removes it
lightbox.classList.contains('open'); // returns true/false
```
This is how the lightbox appears and disappears — the CSS for `.lightbox.open` sets
`opacity: 1`, and JS toggles that class on/off.

### `IntersectionObserver`
Watches elements and fires a callback when they enter or leave the viewport:
```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, { threshold: 0.15 });

observer.observe(myElement);
```
`threshold: 0.15` means: trigger when 15% of the element is visible. This is how
the scroll fade-in animation works — no scroll event listener needed (which would
be slower).

### `document.body.style.overflow = 'hidden'`
Prevents the page from scrolling while the lightbox is open. Resetting it to `''`
restores the default scrolling behavior.

### `e.target === lightbox`
In the lightbox click handler:
```js
lightbox.addEventListener('click', (e) => {
  if (e.target === lightbox) closeLightbox();
});
```
`e.target` is the specific element that was clicked. This check ensures clicking the
dark backdrop closes the lightbox, but clicking the image itself does not.

---

## General Web Concepts

### Semantic Anchor Links
```html
<a href="#about">About</a>
```
The `#about` links to any element with `id="about"`. Combined with
`scroll-behavior: smooth` in CSS, the page glides to that section instead of
jumping.

### Google Fonts
```html
<link href="https://fonts.googleapis.com/css2?family=Orbitron" rel="stylesheet" />
```
Loads a font from Google's servers. Free, no signup. The browser downloads the font
file and uses it for any element where you write `font-family: 'Orbitron', sans-serif`.

### `aria-hidden="true"`
```html
<div class="scanlines" aria-hidden="true"></div>
```
Tells screen readers (used by people with visual impairments) to ignore this element,
since it's purely decorative and has no meaningful content.

### `role="dialog"` and `aria-modal="true"`
```html
<div class="lightbox" role="dialog" aria-modal="true">
```
These accessibility attributes tell assistive technology that this is a dialog window
(the lightbox), so screen readers behave correctly when it's open.

### `loading="lazy"`
```html
<img loading="lazy" />
```
A native browser feature (no JavaScript needed) that delays loading off-screen images
until the user scrolls near them. Speeds up initial page load.

---

## Cheat Sheet: What to Edit and Where

| What you want to change      | File         | What to look for                        |
|------------------------------|--------------|-----------------------------------------|
| Bio text                     | `index.html` | `<!-- ✏️  Edit your bio here -->`        |
| Timeline entries             | `index.html` | `<div class="timeline">`                |
| Stat cards (uni, city, etc.) | `index.html` | `<div class="about-stats">`             |
| Contact links                | `index.html` | `<div class="footer-links">`            |
| Add gallery images           | `index.html` | `<div class="gallery-grid">`            |
| Change colors                | `style.css`  | `:root { }` block at the top            |
| Change fonts                 | `style.css`  | `--font-*` variables in `:root`         |
