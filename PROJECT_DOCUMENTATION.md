# PROJECT DOCUMENTATION — Autono Business Website (Simplified Edition)

> **Audience:** 2nd-year college student preparing for a viva.
> Every line of code is explained in plain English.

---

## 1. Project Overview

### What the webpage does

This is a single-page marketing website for a fictional autonomous (self-driving) car company called **Autono**. A visitor can:

1. Watch a full-screen background video on the first page.
2. Read about the company's vision, services, and technology in scrollable sections.
3. See key statistics (miles driven, cities served, etc.).
4. Pick one of three test drive experiences and book it using a popup form.
5. Subscribe to a newsletter in the footer.

### Files and their roles

| File | Role |
|---|---|
| `index.html` | All HTML structure + inline JavaScript (382 lines) |
| `style.css` | All CSS styling (707 lines, including teaching comments) |
| `arrow.png` | Small arrow image (kept in project but no longer used in HTML) |
| `backup_original/` | Copy of the original files before simplification |
| `CHANGES.md` | Log of everything that was changed and why |
| `PROJECT_DOCUMENTATION.md` | This file |

### How the files connect

```
index.html
  |
  +-- <link href="style.css">         loads the CSS (line 6)
  |     |
  |     +-- @import Google Fonts      downloads "Outfit" font
  |
  +-- <script> block (bottom of body) all JavaScript is here
```

**Loading order:** Browser reads HTML top to bottom. It loads `style.css` first (before rendering the body), then renders each HTML element with styles already applied, then runs the `<script>` block at the very end.

---

## 2. Folder and File Structure

```
Business-website/
  index.html            ← main webpage
  style.css             ← all styles
  arrow.png             ← small arrow icon (kept but unused)
  CHANGES.md            ← simplification log
  PROJECT_DOCUMENTATION.md  ← this file
  backup_original/
    index.html          ← original before changes
    style.css           ← original before changes
    arrow.png           ← original arrow icon
  .git/                 ← Git version control (not part of webpage)
```

---

## 3. HTML Explanation (index.html, line by line)

### Head section (lines 1–8)

```html
<!DOCTYPE html>
```
Not a tag. Tells the browser to use the modern HTML5 standard. Always the first line.

```html
<html lang="en">
```
The root element. `lang="en"` tells screen readers and search engines the page is in English.

```html
<meta charset="UTF-8" />
```
Character encoding: UTF-8 supports all languages and special characters (©, ×, etc.).

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```
Makes the page mobile-friendly. Without this, mobile browsers zoom out and show a tiny desktop layout.

```html
<link rel="stylesheet" href="style.css" />
```
Loads the external CSS file. `href="style.css"` is a relative path — the browser looks in the same folder.

```html
<title>Autono – Safe, Self-Driving Mobility</title>
```
Text shown in the browser tab and in Google search results.

---

### Body section — element by element

---

#### Background Video (lines 14–16)

```html
<video class="bg-video"
  src="https://video.wixstatic.com/.../file.mp4"
  autoplay loop muted></video>
```

| Attribute | What it does |
|---|---|
| `class="bg-video"` | Links to CSS that makes it fill the entire screen |
| `src="https://..."` | URL of the MP4 video on Wixstatic servers |
| `autoplay` | Starts playing immediately on page load |
| `loop` | Restarts when it finishes |
| `muted` | Required for autoplay — browsers block autoplay with sound |

---

#### Navigation Bar (lines 19–25)

```html
<nav class="navbar">
  <span class="brand">AUTONO</span>
  <ul class="nav-links">
    <li>Technology</li>
    <li>About</li>
    <li>Careers</li>
    <li><button class="btn btn-dark" data-open-booking>Book Now</button></li>
  </ul>
</nav>
```

| Element | Purpose |
|---|---|
| `<nav>` | Semantic tag — tells browsers/screen readers this is the navigation region |
| `<span class="brand">` | Brand name. A `<span>` is used (not `<h1>`) because a page should have only one `<h1>` |
| `<ul class="nav-links">` | Horizontal list of links. CSS (`display:flex`) makes it horizontal |
| `<li>Technology/About/Careers</li>` | Plain text items — not real links yet |
| `class="btn btn-dark"` | Two classes: `.btn` gives the shape, `.btn-dark` gives the colour (see Button System) |
| `data-open-booking` | Custom data attribute. JavaScript searches for all elements with this attribute and adds click listeners to them |

---

#### Hero Section (lines 28–37)

```html
<section class="hero">
  <h1>THE FUTURE OF<br />MOBILITY IS HERE</h1>
  <p>Discover the safest self-driving experience with Autono.</p>
  <div class="btn-row">
    <button class="btn btn-dark" data-open-booking>Book a Test Drive</button>
    <a href="#experiences" class="btn btn-outline">Explore Experiences</a>
  </div>
</section>
```

| Element | Purpose |
|---|---|
| `<section class="hero">` | The main hero area, positioned over the video using CSS absolute positioning |
| `<h1>` | The main page headline. There is only **one** `<h1>` per page (good SEO practice) |
| `<br />` | Forces a line break inside the heading |
| `<div class="btn-row">` | A flex container that places the two buttons side by side |
| `<button data-open-booking>` | Opens the booking modal when clicked |
| `<a href="#experiences" class="btn btn-outline">` | An anchor link styled like a button. Scrolls to the `<section id="experiences">` element |

---

#### Vision Section (lines 40–57)

```html
<section class="vision">
  <div class="vision-text">
    <p class="label">VISION</p>
    <h2>We're Changing the Way...</h2>
    <p>Autono is building a future...</p>
  </div>
  <div class="vision-img">
    <img src="https://static.wixstatic.com/..." alt="Autono self-driving car on a city road" />
  </div>
</section>
```

| Element | Purpose |
|---|---|
| `<section class="vision">` | Two-column section (text + image) on a black background |
| `<p class="label">VISION</p>` | Small uppercase label above the heading |
| `<div class="vision-text">` | Left column: label, heading, paragraph |
| `<div class="vision-img">` | Right column: the car photo |
| `alt="Autono self-driving car on a city road"` | Describes the image for screen readers and for when the image fails to load |

---

#### Services Heading (lines 60–64)

```html
<section class="services-head">
  <p class="label">SERVICES</p>
  <h2>We Deliver Exceptional Products...</h2>
</section>
```

A centred heading block introducing the two feature sections below it.

---

#### Autonomous Driving Feature (lines 67–82)

```html
<section class="feature">
  <div class="feature-text">
    <h2>AUTONOMOUS<br />DRIVING</h2>
    <p>Our vehicles navigate cities...</p>
    <button class="btn btn-outline">Read More</button>
  </div>
  <div class="feature-img">
    <img src="https://static.wixstatic.com/..." alt="Autono autonomous driving car" />
  </div>
</section>
```

| Element | Purpose |
|---|---|
| `<section class="feature">` | Two-column section: text left, image right (flexbox row) |
| `<div class="feature-text">` | Left column: heading, paragraph, button |
| `<div class="feature-img">` | Right column: photo |
| `<button class="btn btn-outline">Read More</button>` | Outlined button (no JS action attached yet) |

---

#### Real-Time Information Feature (lines 85–100)

```html
<section class="feature feature-reverse">
  <div class="feature-img"> ... </div>
  <div class="feature-text"> ... </div>
</section>
```

Same two-column layout as Autonomous Driving, but `class="feature-reverse"` adds `flex-direction: row-reverse` in CSS, which puts the image on the LEFT and the text on the RIGHT — without needing a separate HTML layout.

---

#### Why Autono / Parallax Section (lines 103–113)

```html
<section class="why-section">
  <div class="why-card">
    <h2>A different approach...</h2>
    <p>We build every vehicle...</p>
    <button class="btn btn-outline-white">Read More</button>
  </div>
</section>
```

| Element | Purpose |
|---|---|
| `<section class="why-section">` | Full-screen section. Background image set in CSS with `background-attachment:fixed` for parallax effect |
| `<div class="why-card">` | Black rounded card overlaid on the background photo |
| `class="btn btn-outline-white"` | Outlined button with white border (for dark background) |

---

#### Stats Strip (lines 116–123)

```html
<section class="stats" id="stats">
  <div><strong>2M+</strong><span>autonomous miles driven</span></div>
  <div><strong>99.9%</strong><span>incident-free rides</span></div>
  <div><strong>12</strong><span>cities in service</span></div>
  <div><strong>24/7</strong><span>remote safety monitoring</span></div>
</section>
```

| Element | Purpose |
|---|---|
| `<section class="stats">` | Black background strip with 4 stat items side by side |
| `<strong>` | The big number (bold by default, styled to 44px by CSS) |
| `<span>` | The label below the number |

---

#### Experiences Section (lines 126–160)

```html
<section class="experiences" id="experiences">
  <h2>Choose your test drive</h2>
  <p class="sub-text">Each session is 30 minutes...</p>
  <div class="card-grid">
    <article class="card">
      <h3>City Autonomous Ride</h3>
      <p>Navigate traffic lights...</p>
      <p class="card-info">30 min · downtown route · up to 3 guests</p>
      <button class="btn btn-dark" data-open-booking data-exp="City Autonomous Ride">Book this ride</button>
    </article>
    <!-- two more cards follow the same pattern -->
  </div>
</section>
```

| Element | Purpose |
|---|---|
| `id="experiences"` | Target of the `<a href="#experiences">` anchor link in the hero |
| `<div class="card-grid">` | Flex container that places the 3 cards side by side |
| `<article class="card">` | `<article>` is semantic — each card is self-contained, standalone content |
| `data-exp="City Autonomous Ride"` | JavaScript reads this value and pre-selects it in the booking form dropdown |

**Three experience cards:**

| Card | Duration | Route | Max guests |
|---|---|---|---|
| City Autonomous Ride | 30 min | Downtown route | 3 |
| Highway Autopilot | 45 min | Highway loop | 3 |
| Night Safety Demo | 30 min | Closed track | 2 |

---

#### How It Works (lines 163–182)

```html
<section class="how-it-works" id="how">
  <h2>How it works</h2>
  <ol class="steps-list">
    <li>
      <span class="step-no">1</span>
      <h3>Register</h3>
      <p>Pick a ride and fill in a short form.</p>
    </li>
    <!-- steps 2 and 3 follow the same pattern -->
  </ol>
</section>
```

| Element | Purpose |
|---|---|
| `<ol class="steps-list">` | Ordered list (correct semantic choice — the steps have a fixed order). CSS removes the default numbering and replaces it with the styled `<span class="step-no">` |
| `<span class="step-no">1</span>` | The large decorative step number |

---

#### CTA Band (lines 185–190)

```html
<section class="cta-band">
  <h2>Ready to feel the future?</h2>
  <p>Limited slots available this week.</p>
  <button class="btn btn-dark" data-open-booking>Register for Test Drive</button>
</section>
```

Full-width black call-to-action section, centred text. Button opens the booking modal.

---

#### Footer (lines 193–222)

```html
<footer class="site-footer">
  <div class="foot-grid">
    <div><h4>AUTONO</h4><p>Safe, self-driving mobility for everyone.</p></div>
    <div><h4>Visit</h4><p>Coolsingel 1, Rotterdam<br />Mon–Sat, 9:00–18:00</p></div>
    <div><h4>Contact</h4><p>hello@autono.com<br />+31 10 000 0000</p></div>
    <div>
      <h4>Stay updated</h4>
      <form class="news-form" onsubmit="event.preventDefault(); this.innerHTML='<p>Thanks!</p>'">
        <input type="email" placeholder="Your email" aria-label="Email" required />
        <button type="submit" class="btn btn-dark">Subscribe</button>
      </form>
    </div>
  </div>
  <div class="foot-bottom">
    <span>© 2026 Autono. All rights reserved.</span>
    <span><a href="#">Privacy</a> <a href="#">Terms</a></span>
  </div>
</footer>
```

| Element | Purpose |
|---|---|
| `<footer>` | Semantic tag for the page footer |
| `<div class="foot-grid">` | Flex container for 4 equal columns |
| `onsubmit="event.preventDefault(); this.innerHTML='...'"` | Inline JS: stops page reload, then replaces the form HTML with a thank-you message |
| `aria-label="Email"` | Accessibility: screen readers read this label when the user focuses the input |
| `<a href="#">` | Placeholder links for Privacy and Terms (go to page top) |

---

#### Floating Book Button (line 226)

```html
<button class="float-btn btn btn-dark" data-open-booking aria-label="Book a test drive">
  Book a Test Drive
</button>
```

- Hidden by default (`display:none` in CSS).
- JavaScript adds the class `show` (→ `display:block`) when the user scrolls past one full screen height.
- `aria-label` provides a text label for screen readers.

---

#### Booking Modal (lines 229–286)

```html
<div class="modal" id="booking-modal">
  <div class="modal-box" role="dialog" aria-modal="true" aria-labelledby="modal-title">
    <button class="modal-close" aria-label="Close">&times;</button>

    <!-- Form view -->
    <div id="form-wrap">
      <h3 id="modal-title">Register for a Test Drive</h3>
      <p class="modal-note">Limited slots this week...</p>
      <form id="booking-form">
        <input name="name"  type="text"  placeholder="Full name"  required />
        <input name="email" type="email" placeholder="Email"      required />
        <input name="phone" type="tel"   placeholder="Phone"      required />
        <select name="experience" id="exp-select" required>
          <option value="">Select experience</option>
          <option>City Autonomous Ride</option>
          <option>Highway Autopilot</option>
          <option>Night Safety Demo</option>
        </select>
        <div class="form-row">
          <input name="date" type="date" required />
          <select name="time" required>
            <option value="">Time slot</option>
            <option>10:00</option>
            <option>12:00</option>
            <option>14:00</option>
            <option>16:00</option>
          </select>
        </div>
        <label class="consent-label">
          <input type="checkbox" required />
          I agree to be contacted about my booking.
        </label>
        <button class="btn btn-dark" type="submit">Confirm Booking</button>
      </form>
    </div>

    <!-- Success view (hidden until form is submitted) -->
    <div id="booking-success" hidden>
      <h3>Booking received!</h3>
      <p>Thanks — we will confirm your slot by email within 24 hours.</p>
      <button class="btn btn-dark" id="success-close">Close</button>
    </div>
  </div>
</div>
```

**All modal form fields:**

| Field | Tag | `type` | `name` | `required` | Purpose |
|---|---|---|---|---|---|
| Full name | `<input>` | text | name | Yes | Full name |
| Email | `<input>` | email | email | Yes | Contact email |
| Phone | `<input>` | tel | phone | Yes | Phone number |
| Experience | `<select>` | — | experience | Yes | Choose ride (can be pre-selected) |
| Date | `<input>` | date | date | Yes | Pick date |
| Time | `<select>` | — | time | Yes | Pick time slot |
| Consent | `<input>` | checkbox | — | Yes | Consent checkbox |
| Submit | `<button>` | submit | — | — | Submits the form |

**Accessibility attributes:**
- `role="dialog"` — tells screen readers this is a popup dialog
- `aria-modal="true"` — tells screen readers to focus only inside the modal
- `aria-labelledby="modal-title"` — links the dialog to its `<h3 id="modal-title">` heading
- `aria-label="Close"` on the × button — screen readers announce "Close" when focused
- `hidden` attribute on `#booking-success` — hides the div completely (same as `display:none`)

---

### All links, buttons, and forms

**All `<a>` links:**

| Text | href | Goes to |
|---|---|---|
| Explore Experiences | `#experiences` | Scrolls to the experiences section |
| Privacy | `#` | Page top (placeholder) |
| Terms | `#` | Page top (placeholder) |

**All buttons with `data-open-booking`:**

| Button text | Location | `data-exp` value |
|---|---|---|
| Book Now | Navbar | none |
| Book a Test Drive | Hero | none |
| Book this ride | Experience card 1 | City Autonomous Ride |
| Book this ride | Experience card 2 | Highway Autopilot |
| Book this ride | Experience card 3 | Night Safety Demo |
| Register for Test Drive | CTA band | none |
| Book a Test Drive | Floating button | none |

---

## 4. CSS Explanation (style.css, top to bottom)

### Google Fonts (line 1)

```css
@import url("https://fonts.googleapis.com/css2?family=Outfit:wght@100..900&display=swap");
```

Downloads the **Outfit** font from Google before any styles are applied. `display=swap` means the browser shows a system font first while downloading, then swaps to Outfit — so text is never invisible.

---

### Universal Reset (lines 14–21)

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Outfit", sans-serif;
}
```

`*` = every element. This:
- Removes browser default margins/padding (e.g. browsers add a margin to `<body>` by default)
- `box-sizing: border-box` — padding is counted **inside** the element's width, not added on top. With 200px width and 20px padding, the box is still 200px total.
- Sets Outfit as the font everywhere

---

### Background Video (lines 24–32)

```css
.bg-video {
  display: block;
  width: 100vw;
  height: 100vh;
  object-fit: cover;
  z-index: -1;
  position: relative;
}
```

| Property | Value | What it does |
|---|---|---|
| `width: 100vw` | 100% of viewport width | Fills full browser width |
| `height: 100vh` | 100% of viewport height | Fills full browser height |
| `object-fit: cover` | — | Fills the space without distortion; may crop the edges |
| `z-index: -1` | — | Sends the video behind all other content |
| `display: block` | — | Removes the small inline gap below the video element |

---

### Navigation Bar (lines 36–52)

```css
.navbar {
  position: absolute;
  top: 0;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 48px;
  z-index: 2;
}
```

| Property | Value | What it does |
|---|---|---|
| `position: absolute` | — | Floats the navbar on top of the video (taken out of normal document flow) |
| `top: 0` | — | Sticks it to the very top |
| `display: flex` | — | Arranges brand and nav-links side by side |
| `justify-content: space-between` | — | Pushes brand left, links right |
| `z-index: 2` | — | In front of the video (-1) and the hero text (1) |

---

### Button System (lines 72–115)

The entire button system uses **one base class + one modifier class**:

```css
.btn { ... }            /* shape: same for all buttons */
.btn-dark { ... }       /* colour: filled black */
.btn-outline { ... }    /* colour: transparent + black border */
.btn-outline-white { ... } /* colour: transparent + white border */
```

**`.btn` base class properties:**

| Property | Value | What it does |
|---|---|---|
| `padding: 11px 26px` | — | Sets button size |
| `font-size: 15px` | — | Text size |
| `border-radius: 6px` | — | Rounded corners |
| `border: none` | — | Removes browser default button border |
| `cursor: pointer` | — | Shows hand cursor on hover |
| `min-width: 140px` | — | Prevents very narrow buttons |
| `text-decoration: none` | — | Removes underline when `.btn` is applied to an `<a>` tag |
| `transition: background-color 0.25s ease, color 0.25s ease` | — | Hover colour changes animate smoothly |

**`.btn-dark` hover:** background turns from black to orangered  
**`.btn-outline` hover:** background fills black, text turns white  
**`.btn-outline-white` hover:** background fills white, text turns black

---

### Hero Section (lines 119–143)

```css
.hero {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  z-index: 1;
  width: 100%;
  padding: 24px;
}
```

**How the centering trick works:**
1. `top: 40%` → moves the hero's **top edge** to 40% from the top of the viewport
2. `left: 50%` → moves the hero's **left edge** to 50% from the left
3. `transform: translate(-50%, -50%)` → shifts the hero **left** by 50% of its own width and **up** by 50% of its own height

Combined, this places the hero's **centre point** exactly at (50%, 40%) — which centres it horizontally and positions it slightly above the middle of the screen.

---

### Shared Section Styles (lines 147–158)

```css
.vision,
.services-head,
.feature,
.experiences,
.how-it-works,
.cta-band {
  padding: 80px 8%;
  max-width: 1200px;
  margin: 0 auto;
}
```

This grouped selector applies the same padding and width limit to all content sections. `margin: 0 auto` centres the block horizontally when the screen is wider than 1200px.

---

### Vision Section (lines 161–193)

```css
.vision {
  display: flex;
  align-items: center;
  gap: 60px;
  background-color: black;
  color: white;
  max-width: 100%;
  padding: 80px 8%;
}
.vision-text { flex: 1; }
.vision-img   { flex: 1; }
```

`flex: 1` on both columns means they share the available space equally (50/50 split). `gap: 60px` puts 60px of space between them.

---

### Feature Sections (lines 204–237)

```css
.feature { display: flex; align-items: center; gap: 60px; }
.feature-text { flex: 1; }
.feature-img  { flex: 1; }
.feature-reverse { flex-direction: row-reverse; }
```

`.feature-reverse` adds `flex-direction: row-reverse` which flips the order of the flex children — the image appears on the left without changing the HTML order.

---

### Parallax Why Autono Section (lines 240–260)

```css
.why-section {
  height: 100vh;
  background-image: url("https://...");
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  display: flex;
  align-items: center;
  padding: 0 8%;
}
```

`background-attachment: fixed` is the parallax trick. The background image stays **fixed** in place while the browser scrolls the container over it, creating a depth illusion.

---

### Stats, Experiences, How It Works, CTA Band, Footer

All follow the same pattern: flex containers with gaps. Each is explained with a comment block in the CSS file. Refer to the CSS comments for property-level details.

---

### Floating Button (lines 331–343)

```css
.float-btn {
  display: none;          /* hidden by default */
  position: fixed;        /* always in the same screen position, even while scrolling */
  bottom: 24px;
  right: 24px;
  z-index: 10;
}
.float-btn.show {
  display: block;         /* visible when JS adds the "show" class */
}
```

`position: fixed` keeps the button pinned at the bottom-right of the screen as the user scrolls.

---

### Booking Modal (lines 346–405)

```css
.modal {
  display: none;               /* hidden by default */
  position: fixed;             /* covers the whole screen */
  top: 0; left: 0;
  width: 100%; height: 100%;
  background-color: rgba(0,0,0,0.6);  /* semi-transparent dark overlay */
  justify-content: center;     /* these only work when display: flex */
  align-items: center;
  z-index: 100;
}
.modal.open {
  display: flex;               /* flex activates both justify-content and align-items */
}
.modal-box {
  position: relative;          /* needed so .modal-close can be positioned inside it */
  background-color: white;
  width: 440px;
  max-width: 92%;              /* shrinks on small screens so it fits */
  border-radius: 16px;
  padding: 36px;
}
```

**Why `display: none` then `display: flex`?** The `justify-content: center` and `align-items: center` properties only work on flex containers. So the modal must become `display: flex` to centre the white box inside it.

---

### Mobile Media Query (lines 409–432)

```css
@media (max-width: 800px) { ... }
```

Triggered when the screen is **800px or less wide** (phones, small tablets).

| Rule | Effect |
|---|---|
| `flex-direction: column` on vision, feature, stats, card-grid, steps-list, foot-grid | Changes side-by-side to top-to-bottom |
| `.hero h1 { font-size: 38px }` | Shrinks the huge headline so it fits on a small screen |
| Reduced padding on sections | Prevents content from touching the screen edges |
| `background-attachment: scroll` on why-section | Parallax often breaks on mobile; `scroll` is the safe fallback |
| `.nav-links { display: none }` | Hides the nav links (no hamburger menu in this project) |

---

## 5. JavaScript Explanation (inline `<script>`, lines 288–380)

### Variables (lines 289–294)

```javascript
var modal      = document.getElementById("booking-modal");
var bookingForm = document.getElementById("booking-form");
var formWrap   = document.getElementById("form-wrap");
var successDiv = document.getElementById("booking-success");
var expSelect  = document.getElementById("exp-select");
var floatBtn   = document.querySelector(".float-btn");
```

Each variable stores a **reference** to an HTML element so we can change it later.

| Variable | Finds | HTML element |
|---|---|---|
| `modal` | `getElementById("booking-modal")` | The whole modal overlay div |
| `bookingForm` | `getElementById("booking-form")` | The `<form>` element |
| `formWrap` | `getElementById("form-wrap")` | Div containing the heading + form |
| `successDiv` | `getElementById("booking-success")` | Div containing the success message |
| `expSelect` | `getElementById("exp-select")` | The experience `<select>` dropdown |
| `floatBtn` | `querySelector(".float-btn")` | The floating button |

`getElementById` finds an element by its `id`. `querySelector` finds the first element matching a CSS selector.

---

### openModal(clickedBtn) — lines 297–313

```javascript
function openModal(clickedBtn) {
  formWrap.hidden   = false;   // show the form
  successDiv.hidden = true;    // hide the success message

  var experience = clickedBtn.getAttribute("data-exp");
  if (experience) {
    expSelect.value = experience;   // pre-select the dropdown
  }

  modal.classList.add("open");            // show the modal (CSS .modal.open)
  document.body.style.overflow = "hidden"; // prevent page scrolling
}
```

**Purpose:** Shows the modal popup. Called whenever any "Book" button is clicked.

**Step by step:**
1. Show the form (`formWrap.hidden = false`) and hide the success message — so we always start on the form, even if the modal was used before.
2. `clickedBtn.getAttribute("data-exp")` reads the `data-exp` attribute of the button that was clicked.
3. If the button had a `data-exp` value (e.g. `"Highway Autopilot"`), set the dropdown to that value.
4. `modal.classList.add("open")` — adds the CSS class `open` to the modal div. The CSS rule `.modal.open { display: flex; }` then makes it visible.
5. `document.body.style.overflow = "hidden"` — locks the page scroll so only the modal can be scrolled.

---

### closeModal() — lines 316–319

```javascript
function closeModal() {
  modal.classList.remove("open");  // hide the modal
  document.body.style.overflow = ""; // restore page scroll
}
```

Removes the `"open"` class, which causes the modal's CSS to revert to `display: none`.

---

### Attaching click listeners — lines 322–326

```javascript
document.querySelectorAll("[data-open-booking]").forEach(function(btn) {
  btn.addEventListener("click", function() {
    openModal(btn);
  });
});
```

1. `querySelectorAll("[data-open-booking]")` — finds **all** elements that have a `data-open-booking` attribute (7 buttons on the page).
2. `.forEach(...)` — loops through each one.
3. `.addEventListener("click", ...)` — attaches a click handler to each button.
4. When clicked, `openModal(btn)` is called with that specific button as the argument.

---

### Closing the modal — four ways (lines 329–340)

```javascript
// (a) The × button
modal.querySelector(".modal-close").addEventListener("click", closeModal);

// (b) The "Close" button on the success screen
document.getElementById("success-close").addEventListener("click", closeModal);

// (c) Clicking the dark backdrop
modal.addEventListener("click", function(e) {
  if (e.target === modal) {
    closeModal();
  }
});

// (d) Pressing Escape
document.addEventListener("keydown", function(e) {
  if (e.key === "Escape") {
    closeModal();
  }
});
```

For (c): `e.target` is the specific element the user clicked. If they clicked the dark overlay (the `modal` div itself, not the white box inside it), `e.target === modal` is `true` and the modal closes. Clicking inside the white box gives a different `e.target`, so the modal stays open.

---

### Setting the minimum date — line 343

```javascript
bookingForm.date.min = new Date().toISOString().split("T")[0];
```

Step by step:
1. `new Date()` → current date and time object
2. `.toISOString()` → `"2026-10-03T10:16:41.000Z"`
3. `.split("T")` → `["2026-10-03", "10:16:41.000Z"]`
4. `[0]` → `"2026-10-03"` (today's date in YYYY-MM-DD format)
5. `bookingForm.date.min = "2026-10-03"` → the browser disables all past dates in the date picker

`bookingForm.date` accesses the form element whose `name="date"`.

---

### Form submission — lines 346–358

```javascript
bookingForm.addEventListener("submit", function(e) {
  e.preventDefault();

  // TODO: send data to a real server here, e.g.:
  // fetch("https://formspree.io/f/YOUR_ID", { method: "POST", body: new FormData(bookingForm) });

  formWrap.hidden   = true;
  successDiv.hidden = false;
  bookingForm.reset();
});
```

1. `e.preventDefault()` — stops the browser's default form behaviour (which reloads the page).
2. The commented `fetch()` shows where real server-side sending would go.
3. `formWrap.hidden = true` — hides the form.
4. `successDiv.hidden = false` — shows the success message.
5. `bookingForm.reset()` — clears all fields so they are blank if the modal is reopened.

---

### Floating button scroll listener — lines 361–367

```javascript
window.addEventListener("scroll", function() {
  if (window.scrollY > window.innerHeight) {
    floatBtn.classList.add("show");
  } else {
    floatBtn.classList.remove("show");
  }
});
```

- `window.scrollY` — pixels scrolled from the top (0 at the very top).
- `window.innerHeight` — height of the visible browser window in pixels.
- When `scrollY > innerHeight`: the user has scrolled past the first full screen, so the floating button appears.

---

### Execution flow

```
PAGE LOADS
  → DOM variables set (6 var declarations)
  → openModal() and closeModal() defined
  → All 7 [data-open-booking] buttons get click listeners
  → × button, success close button, backdrop click, Escape key all set up
  → Date minimum set to today
  → Scroll listener registered

USER SCROLLS PAST ONE SCREEN HEIGHT
  → floatBtn.classList.add("show") → floating button appears

USER CLICKS A "BOOK" BUTTON
  → openModal(btn) called
    → form shown, success hidden
    → experience pre-selected (if data-exp present)
    → modal.classList.add("open") → modal visible
    → page scroll locked

USER FILLS FORM AND CLICKS "CONFIRM BOOKING"
  → submit event fires
    → e.preventDefault() (no page reload)
    → form hidden, success shown
    → form.reset() clears all fields

USER CLOSES THE MODAL (any of 4 ways)
  → closeModal()
    → modal.classList.remove("open") → modal hidden
    → page scroll restored

USER TYPES EMAIL AND CLICKS "SUBSCRIBE" (footer)
  → onsubmit inline handler fires
    → event.preventDefault() (no reload)
    → this.innerHTML replaced with thank-you text
```

---

## 6. How HTML, CSS, and JS Work Together

| Feature | HTML element | CSS rule | JavaScript |
|---|---|---|---|
| Full-screen video | `<video class="bg-video">` | `width:100vw; height:100vh; z-index:-1` | none |
| Hero text over video | `<section class="hero">` | `position:absolute; top:40%; left:50%; transform:translate(-50%,-50%); z-index:1` | none |
| Navbar over video | `<nav class="navbar">` | `position:absolute; z-index:2` | none |
| Open modal | `<button data-open-booking>` | `.modal.open { display:flex }` | `openModal()` adds `"open"` class |
| Close modal (4 ways) | × button, backdrop, Escape, success Close | `.modal { display:none }` | `closeModal()` removes `"open"` class |
| Experience pre-selection | `data-exp="City Autonomous Ride"` on button | none | `expSelect.value = experience` |
| Form submit → success | `<form id="booking-form">` + `<div id="booking-success" hidden>` | none | `formWrap.hidden=true; successDiv.hidden=false` |
| Floating button | `<button class="float-btn">` | `.float-btn { display:none }` `.float-btn.show { display:block }` | scroll listener adds/removes `"show"` |
| Feature reversed | `<section class="feature feature-reverse">` | `flex-direction: row-reverse` | none |
| Parallax | `<section class="why-section">` | `background-attachment: fixed` | none |
| Newsletter | `<form onsubmit="...">` | `.news-form { display:flex }` | Inline `onsubmit` replaces form with thank-you |

---

## 7. Glossary

| Term | Simple explanation |
|---|---|
| `<!DOCTYPE html>` | Tells the browser to use the modern HTML5 standard |
| Semantic HTML | Using tags that describe meaning (`<nav>`, `<section>`, `<footer>`) not just appearance |
| `<section>` | A block of related content with a heading. Better than `<div>` for main page areas |
| `<article>` | Self-contained content that could stand alone (used for the experience cards) |
| `<nav>` | The navigation region of the page |
| `<footer>` | The bottom information area of the page |
| `viewport` | The visible part of the webpage in the browser window |
| `vw / vh` | Viewport Width / Viewport Height. `100vw` = 100% of the browser window width |
| `px` | Pixel — a fixed unit of measurement |
| `%` | Percentage — relative to the parent element |
| Flexbox | A CSS layout mode that arranges elements in a row or column |
| `display: flex` | Turns a container into a flexbox container |
| `flex: 1` | A flex item grows to fill available space equally with other `flex:1` siblings |
| `justify-content` | Controls spacing along the main axis (horizontal for `flex-direction: row`) |
| `align-items` | Controls alignment on the cross axis (vertical for row) |
| `gap` | Space between flex/grid children |
| `position: absolute` | Removes element from normal flow; positioned relative to the nearest `position: relative` ancestor |
| `position: fixed` | Always positioned relative to the browser window — stays in place when scrolling |
| `z-index` | Stacking order. Higher number = in front |
| `object-fit: cover` | Fills a box with an image/video without distortion; may crop the edges |
| `transform: translate(-50%, -50%)` | Shifts element left by 50% of its own width and up by 50% of its own height |
| `box-sizing: border-box` | Padding included inside the declared width — avoids unexpected size overflow |
| `transition` | Animates a CSS property change over time. `0.25s ease` = 250 ms with a smooth curve |
| `background-attachment: fixed` | Parallax effect — background image stays still while the element scrolls over it |
| `:hover` | CSS pseudo-class: styles applied only when the mouse is over the element |
| `@media (max-width: 800px)` | Media query: rules inside only apply when screen width ≤ 800px |
| `@import` | Loads another CSS file or font from a URL |
| DOM | Document Object Model — the browser's JavaScript-accessible tree of all HTML elements |
| `document.getElementById` | Returns the element with the given `id` |
| `document.querySelector` | Returns the first element matching a CSS selector |
| `document.querySelectorAll` | Returns ALL elements matching a CSS selector (as a NodeList) |
| `addEventListener` | Attaches a function to run when an event (click, scroll, keydown) happens |
| `classList.add / remove` | Adds or removes a CSS class on an element |
| `e.preventDefault()` | Stops the browser's default action (e.g. stops a form from reloading the page) |
| `e.target` | The exact element the user interacted with inside an event |
| `element.hidden` | Setting to `true` hides the element; `false` shows it (equivalent to `display:none`) |
| `window.scrollY` | How many pixels the user has scrolled down from the top |
| `window.innerHeight` | The height of the visible browser window in pixels |
| `new Date().toISOString().split("T")[0]` | Gets today's date as a string in `YYYY-MM-DD` format |
| `form.reset()` | Clears all form fields back to their default values |
| `data-*` attribute | Custom HTML attribute. Used to store extra information that JS can read with `getAttribute` |
| ARIA attributes | Accessibility attributes (`aria-label`, `role`, `aria-modal`) that help screen readers |

---

## 8. Viva / Presentation Prep

### 20 questions with answers based on the actual code

**Q1. What is the purpose of the website?**
A single-page marketing site for Autono, a fictional self-driving car company. Visitors can read about the technology and book a test drive through a popup form.

**Q2. How many files does the project use?**
Two working files: `index.html` and `style.css`. The JavaScript is inline inside `index.html` in a `<script>` block at the bottom.

**Q3. Why is the `<script>` tag at the bottom of `<body>`?**
So all the HTML elements exist in the DOM before JavaScript tries to access them with `getElementById`. If the script ran from `<head>`, the elements would not exist yet and `getElementById` would return `null`.

**Q4. Why is `<nav>` used instead of `<div class="navbar">`?**
`<nav>` is a semantic element — it tells browsers, search engines, and screen readers that this region contains navigation links. A `<div>` has no semantic meaning.

**Q5. Explain `transform: translate(-50%, -50%)` on `.hero`.**
`top: 40%; left: 50%` moves the hero's top-left corner to that position. But we want the hero's **centre** there. Translating by `-50%` of its own width (left) and `-50%` of its own height (up) shifts the centre point to the correct location.

**Q6. How does the button system work?**
Every button uses `class="btn"` for shared shape (padding, font-size, border-radius, transition). A second modifier class sets the colour: `btn-dark` = black fill, `btn-outline` = transparent with black border, `btn-outline-white` = transparent with white border.

**Q7. What does `data-open-booking` do?**
It is a custom data attribute that marks a button as a booking trigger. JavaScript uses `querySelectorAll("[data-open-booking]")` to find all such elements and attach click listeners.

**Q8. What does `data-exp="City Autonomous Ride"` do?**
Inside `openModal()`, JavaScript calls `clickedBtn.getAttribute("data-exp")` to read this value, then sets `expSelect.value = experience` to pre-select that option in the booking form dropdown.

**Q9. How is the modal shown and hidden?**
`modal.classList.add("open")` adds the CSS class `open`. The rule `.modal.open { display: flex; }` makes it visible. `modal.classList.remove("open")` removes the class and the modal reverts to `display: none`.

**Q10. Why is `document.body.style.overflow = "hidden"` called?**
To prevent the page behind the modal from scrolling while the modal is open. `overflow: hidden` on the `<body>` locks vertical scrolling. Setting it back to `""` restores normal scrolling.

**Q11. What are the four ways to close the modal?**
1. Click the × button, 2. Click the dark overlay (backdrop), 3. Press the Escape key, 4. Click the "Close" button on the success screen.

**Q12. How does clicking outside the modal close it?**
The click listener on the `.modal` div checks `if (e.target === modal)`. If the user clicked the dark overlay div itself, `e.target` equals the modal and `closeModal()` runs. Clicking inside the white box gives a different `e.target`, so nothing happens.

**Q13. How is the minimum date set in the booking form?**
`new Date().toISOString()` gives `"2026-10-03T10:..."`. `.split("T")[0]` extracts `"2026-10-03"`. This string is assigned to `bookingForm.date.min`, which makes the browser disable all past dates in the date picker.

**Q14. What happens when the booking form is submitted?**
`e.preventDefault()` stops the page reload. Then `formWrap.hidden = true` hides the form, `successDiv.hidden = false` shows the success message, and `bookingForm.reset()` clears all fields.

**Q15. How does the floating "Book" button appear?**
A `scroll` event listener runs on every scroll. If `window.scrollY > window.innerHeight` (user scrolled past one full screen), `floatBtn.classList.add("show")` is called. CSS `.float-btn.show { display: block; }` makes the button visible.

**Q16. What is `flex-direction: row-reverse` used for?**
The `.feature-reverse` class adds this to the second feature section. It reverses the order of the flex children so the image appears on the LEFT and the text on the RIGHT — without changing the HTML structure.

**Q17. How does parallax work in `.why-section`?**
`background-attachment: fixed` tells the browser to keep the background image fixed relative to the viewport (not the element). As the user scrolls, the element moves but the image stays still, creating a depth illusion.

**Q18. What does `e.preventDefault()` do in the newsletter form?**
It stops the browser's default form submit action (which would navigate to a URL or reload the page). The inline `onsubmit` attribute then replaces the form's HTML with a thank-you paragraph.

**Q19. What is `aria-labelledby="modal-title"` on the modal box?**
It links the dialog to its heading (`<h3 id="modal-title">`). When a screen reader opens the modal, it reads the heading text aloud so visually impaired users know what the dialog is about.

**Q20. Name two bugs that were fixed from the original code.**
1. `rgba(0,0,0,190.5)` — alpha value 190.5 is invalid (must be 0–1). Fixed by removing the whole section. 2. `var float = querySelector(...)` — `float` is a reserved word; renamed to `floatBtn`. Also: `function open()` shadowed `window.open`; renamed to `openModal()`.

---

### 2-Minute Presentation Script

"Hello. This project is a single-page marketing website for a fictional self-driving car company called Autono.

The first thing a visitor sees is a full-screen looping video. Over it, the navigation bar and a large headline — 'The Future of Mobility is Here' — are layered using CSS absolute positioning and z-index to control what appears in front.

Scrolling down, the page shows the company vision, two feature sections, a parallax background section, a black stats strip, three experience booking cards, a how-it-works section, and a call-to-action banner. The footer has four columns and a newsletter form.

The main interactive feature is the booking modal. Any button with the attribute `data-open-booking` opens it. JavaScript uses `querySelectorAll` to find all seven such buttons and attach click listeners. When clicked, the `openModal` function adds an `open` class to the modal div, which triggers a CSS rule that makes it visible. The function also reads a `data-exp` attribute to pre-select the correct ride type in the form dropdown.

The form validates all fields using the `required` attribute. On submit, `e.preventDefault()` stops the page reload, then JavaScript hides the form and shows a success message. There are four ways to close the modal: the × button, clicking the dark backdrop, pressing Escape, and the success-screen Close button.

The CSS uses a unified button system: every button shares one `.btn` class for shape and uses a modifier class — `.btn-dark` or `.btn-outline` — for colour only. This keeps the design consistent and the CSS shorter.

One responsive media query handles screens under 800px by stacking layouts vertically, shrinking the headline, and reducing padding. Thank you."

---

## 9. Known Limitations

| Issue | Status |
|---|---|
| Form does not send data to a server | A `fetch()` call is commented out inside the submit handler. Integrate Formspree or EmailJS to fix. |
| Privacy and Terms links go to `#` (page top) | Placeholder links — real policy pages are not created |
| "Read More" buttons on feature sections have no action | No JS is attached; they are UI placeholders |
| Technology, About, Careers nav items are plain text | Not linked to real pages |
| Nav links hidden on mobile with no hamburger menu | A proper hamburger menu would require more HTML and JS |
| `arrow.png` is still in the project folder | No longer used in the HTML — can be deleted |
