# CHANGES.md – Simplification Log

## What was done first
The original files were copied to `backup_original/` before any changes.

---

## Final line counts

| File | Original | New (total) | New (code only, no comments/blanks) |
|---|---|---|---|
| `index.html` | 287 | 382 | 295 |
| `style.css` | 756 | 707 | 569 |
| **Total code lines** | **1,043** | | **864** |

The extra lines in the totals are teaching comments — plain-English explanations above every section. These are intentional: they help a student understand the code without opening any other document.

---

## HTML changes

### Removed
| What | Why |
|---|---|
| `<div class="hero2">` and its `.line` / `.line2` decorative divs | Pure decoration with no content value; added complexity for no benefit |
| `<div class="hero3">` (Services) | Was just a heading with two decorative `<div>` lines; replaced with a clean `<section class="services-head">` |
| `<div class="auto-dri">` wrapper | Replaced with semantic `<section class="feature">` |
| `<div class="hero4">` wrapper | Replaced with `<section class="feature feature-reverse">` using CSS row-reverse instead of a separate HTML layout |
| `<div class="WhyAutono">` and `.WhyAutono-container` / `.WhyAutono-content` | Three nested divs collapsed into `<section class="why-section">` + `<div class="why-card">` |
| `<div class="hero-cta">` inside CTA band | Not needed; the `.cta-band` itself is centred via `text-align:center` |
| Arrow `<img>` inside "Read More" buttons | Removed: the arrow icon (`arrow.png`) inside a button is a non-standard pattern that confuses students and is not needed |
| Placeholder `<br>` tags in long paragraphs | Replaced with real, meaningful sentences |
| `<div class="line1">` and its empty inner `<div>` | Pure decoration; removed |
| `id="stats"` (unused by JS or CSS) | Kept only the IDs actually referenced: `#experiences` (anchor link), `#how` (anchor), and the modal IDs |

### Changed
| What | What it changed to | Why |
|---|---|---|
| `<div class="navbar">` | `<nav class="navbar">` | Semantic HTML: `<nav>` tells browsers/screen readers this is a navigation region |
| `<h1>AUTONO</h1>` (brand name in navbar) | `<span class="brand">AUTONO</span>` | A page should have only one `<h1>`; a brand name in a nav is better as a `<span>` |
| `<div class="hero1">` | `<section class="hero">` | Semantic + consistent naming |
| `<h2>` for the hero headline | `<h1>` | The main page headline should be `<h1>` for SEO and accessibility |
| `alt="error"` on images | Descriptive alt text | Screen readers read "error" aloud — that is wrong |
| `alt=""` on feature images | Descriptive alt text | All meaningful images need descriptive alt text |
| `<title>Background Video</title>` | `<title>Autono – Safe, Self-Driving Mobility</title>` | The tab and search results showed the wrong name |
| `<div class="hero-cta">` button rows | `<div class="btn-row">` | Clearer, reusable class name |
| `btn-primary` / `btn-book` / `btn-outline` | Unified `.btn` system (see below) | Consistency — one system is easier to understand and maintain |
| `var float = …` in JS | `var floatBtn = …` | `float` is a reserved word in JavaScript; renamed to avoid a potential bug |
| `function open()` | `function openModal()` | `open` is a built-in `window.open` function; renaming avoids shadowing it |
| `function close()` | `function closeModal()` | Same reason as above |
| `window.scrollY > window.innerHeight * 0.8` | `window.scrollY > window.innerHeight` | Simpler threshold; shows the button after one full screen of scrolling |
| Inline `onsubmit` on the newsletter form | Kept as-is | Already simple and clear; no JavaScript change needed |

---

## CSS changes

### Removed selectors / rules

| Removed | Why |
|---|---|
| `.line`, `.line2`, `.line1` | Decorative only; HTML elements also removed |
| `.hero2`, `.hero3`, `.hero4`, `.ser-line`, `.ser-line2`, `.ser-head` | HTML sections replaced with cleaner equivalents |
| `.auto-dri`, `.auto-head`, `.auto-img`, `.auto-head div`, `.auto-head button`, `.auto-head div img`, `.auto-head div img:hover` | Replaced by `.feature`, `.feature-text`, `.feature-img` |
| `.text-4`, `.text-4 h1`, `.text-4 p`, `.text-4 div`, `.text-4 div img`, `.text-4 div button` | Same as above |
| `.WhyAutono`, `.WhyAutono-container`, `.WhyAutono-container .line1`, `.WhyAutono-container .line1 div`, `.WhyAutono-content`, `.WhyAutono-content h1`, `.WhyAutono-content p`, `.WhyAutono-content button`, `.WhyAutono-content button img` | Replaced by `.why-section` and `.why-card` |
| `.hero1` | Replaced by `.hero` |
| `.btn-primary`, `.btn-book`, `ul li button.btn-book` | Replaced by the unified `.btn` system |
| `.hero-cta` | Replaced by `.btn-row` |
| `.faq` (in grouped selectors) | No `.faq` element exists in the HTML; was unused |
| `ul` (bare selector) | Too broad; replaced by `.nav-links` |
| `ul li`, `ul li:hover`, `ul li button`, `ul li button:hover` | Replaced by `.nav-links li` etc. |
| `.news-form button` (separate rule) | The newsletter Subscribe button now uses `.btn.btn-dark` |
| Poppins font import | Poppins was imported but never used; removed to save a network request |

### Fixed bugs

| Bug | Fix |
|---|---|
| `box-shadow: 0 -50px 100px 50px rgba(0,0,0,190.5)` on `.hero2` | Alpha value 190.5 is invalid (must be 0–1). Entire hero2 section removed. |
| `box-shadow: 1 -50px 0px 200px white` on `.hero3` | Horizontal offset `1` has no unit (should be `1px`). Entire hero3 section removed. |
| `display: flex` declared twice in `.hero2` and `.vision` | Duplicates removed |
| `font-size: 1.5rem; font-size: 40px;` in `.auto-head h2` | Second overrides first; first removed |
| `line-height: 1.6; line-height: 33px;` in `.auto-head p` | Second overrides first; first removed |
| `font-weight: 200; font-weight: 300;` in `.auto-head p` | Second overrides first; first removed |
| `letter-spacing: 3px; letter-spacing: 1px;` in `.ser-head p` | Second overrides first; first removed |
| `transition` only on `:hover` (not base rule) | Hover-out had no transition; fixed by putting `transition` on `.btn` base class |
| `var float = querySelector(...)` shadows reserved word | Renamed to `floatBtn` |
| `function open(e)` shadows `window.open` | Renamed to `openModal(clickedBtn)` |

### Merged / unified

| Before | After |
|---|---|
| `.experiences`, `.how`, `.faq`, `.cta-band` shared padding rule (with unused `.faq`) | Single shared list on relevant sections; `.faq` removed |
| `.btn-primary` and `.btn-outline` had separate padding, font-size, border-radius | All buttons use `.btn` for shared shape; `.btn-dark` / `.btn-outline` / `.btn-outline-white` for colour only |
| `.auto-head div` and `.text-4 div` had identical button + border styles | Both sections replaced with `.feature-text` |

---

## How the button system works

Every button on the page uses **two classes**:

```
class="btn btn-dark"          ← filled black button (turns orangered on hover)
class="btn btn-outline"       ← transparent with black border (fills black on hover)
class="btn btn-outline-white" ← transparent with white border (for dark backgrounds)
```

The **`.btn` class** sets properties that are the same for every button:
- `padding: 11px 26px` – the size
- `font-size: 15px` – the text size
- `border-radius: 6px` – the corner rounding
- `min-width: 140px` – a minimum width so buttons are never too narrow
- `transition: ...` – smooth colour change on hover
- `cursor: pointer` – shows a hand cursor

The **modifier classes** only change colours:
- `.btn-dark` → `background-color: black; color: white;`
- `.btn-outline` → `background: transparent; border: 1px solid black; color: black;`
- `.btn-outline-white` → `background: transparent; border: 1px solid white; color: white;`

The `<a>` tag used for "Explore Experiences" also gets `class="btn btn-outline"` and `text-decoration: none` removes the underline.

---

## What was kept (unchanged in purpose)

- Background video, navbar, hero text, vision, feature sections, Why Autono parallax, stats strip, experience cards, how-it-works steps, CTA band, footer, newsletter form, floating button, booking modal, all JavaScript modal logic.
- Colour scheme: black, white, orangered.
- The single `@media (max-width: 800px)` responsive breakpoint.
