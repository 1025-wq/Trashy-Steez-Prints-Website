# Trashy Steez Prints — Full Website Build Brief
> Paste this entire document into Claude Code as your build prompt.

---

## 1. PROJECT OVERVIEW

Build a **single-page website** for **Trashy Steez Prints**, a South African fabric & product printing company that produces branded merchandise and campaign items for businesses. The site must be production-ready HTML, CSS, and vanilla JavaScript (no frameworks required — keep it a single `index.html` file with embedded CSS and JS unless you prefer to split into `style.css` and `script.js`).

### Core business
- Prints on fabric and hard goods: t-shirts, hoodies, caps, tote bags, water bottles, banners, and more
- Primary customers: companies running branded campaigns and merchandise
- Secondary customers: individuals and small groups
- Location: South Africa
- WhatsApp number: **+27 68 057 0848** (primary sales channel)

### Must-have features
1. Instant quote calculator (multi-step wizard)
2. WhatsApp floating button + quote-to-WhatsApp handoff
3. Portfolio/lookbook gallery
4. B2B "For Companies" section
5. Fully responsive — mobile-first, works on 375px screens

---

## 2. BRAND IDENTITY & AESTHETIC

### Aesthetic direction: "Industrial Neon — Factory Rave"
This is not a generic print shop. The aesthetic is **heavy industrial machinery meets electric neon** — like a rave happening inside a real factory. The two hero photos (actual printing equipment and sewing workshop) establish immediate credibility and power. The neon cyan from the logo is the electric layer on top of the raw industrial grit. Think: Detroit factory floor at midnight, lit by neon signs.

**The unforgettable moment**: When a visitor lands on the page, they're looking DOWN at a real professional screen-printing carousel — massive blue industrial machines from above. The text "WE MAKE YOUR BRAND LOUD" floats over it in giant Bebas Neue with neon glow. It's visceral. It says: these people are serious.

**What makes this different from every other SA printer's site**: They all have stock photos of smiling people holding t-shirts. We have the actual machines. The actual workshop. Real equipment, real craft — and it's dressed in neon.

### Logo
The logo is a **circular badge** on a deep navy/near-black background featuring:
- "TRASHY STEEZ" in chunky, glow-lit text
- The iconic "man throwing object in bin" symbol, rendered as a glowing neon icon
- Everything glows in electric cyan/blue neon — like a real neon sign

Use the logo as a PNG if provided, or recreate it using SVG with a circular crop and cyan neon text effect. Place it in the navbar and hero.

### Color palette (exact CSS variables to use)
```css
:root {
  --color-bg:         #05091a;   /* deep navy, near-black */
  --color-surface:    #0c1330;   /* slightly lighter navy for cards/surfaces */
  --color-surface-2:  #111a3a;   /* hover state / elevated surface */
  --color-cyan:       #00d4ff;   /* primary neon cyan — CTAs, accents, glows */
  --color-cyan-dim:   #00a8cc;   /* dimmer cyan for secondary text links */
  --color-white:      #f0f8ff;   /* slightly blue-tinted white for body text */
  --color-muted:      #7a9ab5;   /* muted blue-grey for labels and secondary text */
  --color-border:     rgba(0, 212, 255, 0.15); /* subtle cyan border */
  --color-border-bright: rgba(0, 212, 255, 0.4); /* hover border */
  --glow-cyan:        0 0 20px rgba(0, 212, 255, 0.4), 0 0 40px rgba(0, 212, 255, 0.15);
  --glow-cyan-strong: 0 0 30px rgba(0, 212, 255, 0.6), 0 0 60px rgba(0, 212, 255, 0.25);
}
```

### Typography
- **Display / headings**: `"Bebas Neue"` from Google Fonts — bold, tall, condensed. Perfect for the streetwear feel.
- **Body / UI text**: `"DM Sans"` from Google Fonts — clean and readable at small sizes.
- **Accent/tagline**: `"Space Mono"` from Google Fonts — monospaced techy feel for price displays and step counters.

Load all three from Google Fonts:
```html
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@400;500;600&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
```

Typography scale:
```css
--text-hero:    clamp(64px, 12vw, 140px);  /* hero headline */
--text-h2:      clamp(36px, 6vw, 72px);    /* section titles */
--text-h3:      clamp(22px, 3vw, 32px);    /* card titles, subsections */
--text-body:    16px;
--text-small:   14px;
--text-label:   12px;
```

### Neon glow effect
Apply `text-shadow: var(--glow-cyan)` to Bebas Neue headings in accent sections. Apply `box-shadow: var(--glow-cyan)` to primary CTA buttons and the active quote wizard step. This is the signature visual — use it deliberately, not on everything.

---

## 3. PAGE STRUCTURE

The site is a **single scrolling page** with a sticky nav. Sections in order:

1. `#hero` — Full-screen landing
2. `#products` — Product catalogue grid
3. `#quote` — Instant quote calculator wizard
4. `#how-it-works` — 3-step process
5. `#portfolio` — Campaign lookbook gallery
6. `#for-companies` — B2B section
7. `#trust` — Social proof strip
8. `#contact` — Final CTA + contact info
9. Floating WhatsApp button (fixed position, always visible)
10. Footer

---

## 4. SECTION SPECS

### 4.1 NAVBAR

Sticky top nav, `position: sticky; top: 0; z-index: 100`.

- Background: `rgba(5, 9, 26, 0.9)` with `backdrop-filter: blur(12px)` for glassmorphism effect
- Left: Trashy Steez logo (circular badge, ~48px height)
- Center: Nav links — Products | Quote | Portfolio | For Companies | Contact
- Right: "GET A QUOTE" button (cyan bordered, glows on hover) + WhatsApp icon button
- On mobile (< 768px): hamburger menu, full-screen overlay nav with large Bebas Neue links
- Nav links in DM Sans 14px, spaced out, uppercase, letter-spacing 0.1em
- Active section link gets cyan color

### 4.2 HERO SECTION

Full viewport height (`100vh`). **Background is `photo-factory.jpg`** — the overhead industrial screen printing carousel shot. This is the anchor image of the entire site.

**Photo treatment:**
```css
#hero {
  background-image: url('photo-factory.jpg');
  background-size: cover;
  background-position: center top;
  position: relative;
}
/* Layer 1: deep dark overlay so text pops */
#hero::before {
  content: '';
  position: absolute; inset: 0;
  background: linear-gradient(
    to bottom,
    rgba(5, 9, 26, 0.70) 0%,
    rgba(5, 9, 26, 0.50) 50%,
    rgba(5, 9, 26, 0.85) 100%
  );
  z-index: 1;
}
/* Layer 2: cyan color-grade tint — makes factory blues match brand */
#hero::after {
  content: '';
  position: absolute; inset: 0;
  background: rgba(0, 60, 100, 0.20);
  mix-blend-mode: color;
  z-index: 2;
}
#hero > * { position: relative; z-index: 3; }
```

**Layout — ASYMMETRIC, not centred:**
Text anchors to **bottom-left** (not centered). This is unexpected and more editorial/magazine than a typical print shop.
```css
.hero-content {
  position: absolute;
  bottom: 15%;
  left: 8%;
  max-width: 700px;
}
```

**Content (bottom-left anchored):**
- Top: Small uppercase monospace label — `// SOUTH AFRICA'S BOLDEST PRINT STUDIO` (cyan, 11px letter-spacing: 0.15em)
- Main headline in Bebas Neue:
  ```
  WE MAKE
  YOUR BRAND
  LOUD.
  ```
  Lines 1–2: white. `LOUD.` alone on line 3 — full cyan with `text-shadow: var(--glow-cyan-strong)`. Make it massive: `clamp(80px, 14vw, 160px)`.
- Subtext in DM Sans: `T-shirts · Hoodies · Caps · Bottles · Bags · And more`
- Two CTA buttons:
  - Primary: `GET AN INSTANT QUOTE` — filled cyan, dark text, glow on hover
  - Secondary: `CHAT ON WHATSAPP` — outlined, white text
- Bottom of hero: Animated scroll-down indicator

**Grain overlay (adds texture and depth — critical for the industrial feel):**
```css
.grain-overlay {
  position: fixed; inset: 0; z-index: 0; pointer-events: none;
  opacity: 0.035;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  background-repeat: repeat;
  background-size: 256px 256px;
}
```
Add `<div class="grain-overlay" aria-hidden="true"></div>` as the first child of `<body>`. This is the detail that separates a designed site from an AI-generated one.

### 4.3 PRODUCTS SECTION

Section title: `"THE CATALOGUE"` in Bebas Neue, with subtitle `"We print on everything."` in DM Sans.

**Grid layout:** 3 columns desktop → 2 columns tablet → 1 column mobile.

**Product cards** (8 total):

| ID | Product | Emoji placeholder | Starting from |
|----|---------|-------------------|---------------|
| 1 | T-Shirts | 👕 | R85/unit |
| 2 | Hoodies | 🧥 | R220/unit |
| 3 | Caps | 🧢 | R75/unit |
| 4 | Tote Bags | 👜 | R55/unit |
| 5 | Water Bottles | 🧴 | R95/unit |
| 6 | Banners | 🏳️ | R180/unit |
| 7 | Work Shirts | 👔 | R110/unit |
| 8 | Custom Items | ✨ | Get a quote |

Each card:
- Background: `var(--color-surface)`, border `var(--color-border)`
- On hover: border brightens to `var(--color-border-bright)`, subtle translateY(-4px) lift (transform only, 200ms ease-out)
- Shows: large icon/illustration area (top half, dark bg), product name in Bebas Neue, "from R[price]" in Space Mono cyan, "GET QUOTE →" link in cyan
- Click on any card scrolls to #quote with that product pre-selected

### 4.4 GET AN INSTANT QUOTE (simple enquiry form — no price estimation)

Section title: `"GET AN INSTANT QUOTE"` + subtitle `"Fill in your details — we'll come back to you fast."`

**No multi-step wizard. No price calculations. Just a clean, single-page form** that collects the order details and fires them straight to WhatsApp.

**Form fields:**

```html
<form id="quote-form" novalidate>

  <div class="form-row">
    <label for="q-name">Your name</label>
    <input type="text" id="q-name" name="name" placeholder="e.g. Thabo" autocomplete="name" required>
  </div>

  <div class="form-row">
    <label for="q-phone">WhatsApp / phone number</label>
    <input type="tel" id="q-phone" name="phone" placeholder="+27 ..." inputmode="tel" autocomplete="tel" required>
  </div>

  <div class="form-row">
    <label for="q-product">What do you need printed?</label>
    <select id="q-product" name="product" required>
      <option value="" disabled selected>Select a product</option>
      <option>T-Shirts</option>
      <option>Hoodies</option>
      <option>Caps</option>
      <option>Tote Bags</option>
      <option>Water Bottles</option>
      <option>Banners</option>
      <option>Work Shirts</option>
      <option>Other / Not sure</option>
    </select>
  </div>

  <div class="form-row">
    <label for="q-qty">Approximate quantity</label>
    <select id="q-qty" name="quantity" required>
      <option value="" disabled selected>Select quantity</option>
      <option>1 – 10 units</option>
      <option>10 – 50 units</option>
      <option>50 – 100 units</option>
      <option>100 – 250 units</option>
      <option>250 – 500 units</option>
      <option>500+ units</option>
    </select>
  </div>

  <div class="form-row">
    <label for="q-method">Print method (if you know)</label>
    <select id="q-method" name="method">
      <option value="" selected>Not sure — advise me</option>
      <option>Screen Print</option>
      <option>Embroidery</option>
      <option>DTG (Direct to Garment)</option>
      <option>Heat Transfer</option>
    </select>
  </div>

  <div class="form-row">
    <label for="q-notes">Anything else we should know?</label>
    <textarea id="q-notes" name="notes" rows="3"
      placeholder="e.g. deadline, colours, artwork ready or not..."></textarea>
  </div>

  <button type="submit" class="btn-primary btn-glow">
    SEND TO WHATSAPP →
  </button>

</form>
```

**Submit handler — builds WhatsApp message from form data, no pricing:**

```js
document.getElementById('quote-form').addEventListener('submit', function(e) {
  e.preventDefault();
  const f = e.target;

  // Basic validation
  if (!f.name.value.trim() || !f.phone.value.trim() || !f.product.value) {
    // Highlight empty required fields — add .error class, remove on input
    return;
  }

  const msg = [
    'Hi Trashy Steez! I\'d like to get a quote:',
    '',
    `Name: ${f.name.value.trim()}`,
    `Phone: ${f.phone.value.trim()}`,
    `Product: ${f.product.value}`,
    `Quantity: ${f.quantity.value}`,
    `Print method: ${f.method.value || 'Not sure — please advise'}`,
    f.notes.value.trim() ? `Notes: ${f.notes.value.trim()}` : null,
  ].filter(Boolean).join('\n');

  window.open('https://wa.me/27680570848?text=' + encodeURIComponent(msg), '_blank');
});
```

**Form styling (matches the work-order aesthetic):**
```css
#quote-form { max-width: 560px; margin: 0 auto; }

.form-row { margin-bottom: 20px; }

.form-row label {
  display: block; margin-bottom: 6px;
  font-family: 'Space Mono', monospace;
  font-size: 11px; letter-spacing: 0.1em;
  color: var(--color-cyan); text-transform: uppercase;
}

.form-row input,
.form-row select,
.form-row textarea {
  width: 100%; min-height: 44px; padding: 12px 16px;
  font-size: 16px; font-family: 'DM Sans', sans-serif;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  color: var(--color-white);
  border-radius: 4px;
  transition: border-color 0.2s ease-out;
  appearance: none; -webkit-appearance: none;
}

.form-row input:focus,
.form-row select:focus,
.form-row textarea:focus {
  outline: none;
  border-color: var(--color-cyan);
  box-shadow: 0 0 0 2px rgba(0,212,255,0.15);
}

.form-row input.error,
.form-row select.error {
  border-color: #ff4d4d;
}

/* Custom select arrow in cyan */
.form-row select {
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%2300d4ff' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 14px center;
  padding-right: 40px;
}
```

**No Supabase logging needed for this form** (it was tied to the wizard). The WhatsApp message carries all the data. Remove the `logQuoteRequest()` call from Section 13.

### 4.5 BEHIND THE PRINT (new section — insert between How It Works and Portfolio)

This section uses **`photo-workshop.jpg`** — the sewing workshop with coloured thread spools and branded garments being worked on. It's the human side of the operation.

**Layout — full-bleed 2-column split:**
```
[ LEFT: photo-workshop.jpg (50% width) ]  [ RIGHT: text content (50% width) ]
```
On mobile: photo on top, text below.

**Photo treatment (left):**
```css
.workshop-photo {
  width: 100%; height: 100%; min-height: 600px;
  object-fit: cover; object-position: center;
  filter: brightness(0.75) contrast(1.05) saturate(0.7);
  /* Desaturate slightly → the cyan text on the right pops harder */
}
```
Add a right-edge gradient fade so the photo bleeds into the right panel:
```css
.workshop-col::after {
  content: '';
  position: absolute; top: 0; right: 0; bottom: 0; width: 120px;
  background: linear-gradient(to right, transparent, var(--color-bg));
}
```

**Text content (right side):**
- Section label (Space Mono, cyan, 11px): `// THE CRAFT`
- Headline (Bebas Neue): `EVERY THREAD. EVERY COLOUR. EVERY CAMPAIGN.`
- Body text: `We're not resellers. Every item is produced in-house — from the first stitch to the final print. That's why the quality is consistent, and why we can promise fast turnaround.`
- Three stat blocks:
  - `500+` / campaigns completed
  - `48hr` / average turnaround
  - `100%` / in-house production
- CTA: `SEE OUR WORK ↓` (scrolls to portfolio)

### 4.5b HOW IT WORKS

Section title: `"AS EASY AS 1, 2, 3"`

Three horizontal steps (stack vertically on mobile):

1. **GET YOUR QUOTE** — Use our instant calculator or chat to us on WhatsApp with your idea.
2. **SEND YOUR ARTWORK** — Drop us your logo or design. No artwork? We can help create it.
3. **WE DELIVER** — We print your order and deliver nationwide across South Africa.

Each step: large step number in Bebas Neue (180px, very faint cyan), icon, title, description. Connected by a dashed line on desktop (hide on mobile).

**Background for this section:** Use `bg-quote.jpg` (the plasma wave) with 80% dark overlay — it adds depth without competing with the step content.

### 4.6 PORTFOLIO — THE LOOKBOOK

Section title: `"THE WORK"` + subtitle `"Campaigns we've brought to life."`

**Filter tabs** (above the grid): `ALL | T-SHIRTS | CAPS | HOODIES | BOTTLES | CAMPAIGNS`

**Masonry-style grid** (or CSS columns) with placeholder project cards. Use 8–10 placeholder items. Each item:
- Background: `var(--color-surface)` with a large emoji or `[PHOTO]` placeholder
- On hover: overlay slides in from bottom with project name + client type (e.g., "Corporate Campaign", "Event Merch")
- Click: could expand to a lightbox (nice-to-have) or just show the overlay

Placeholder projects (use placeholder boxes with these labels):
1. "Summer Campaign Tees" — 200 units
2. "Tech Company Caps" — 500 units  
3. "NGO Awareness Hoodies" — 150 units
4. "Brand Water Bottles" — 300 units
5. "Retail Uniform Shirts" — 80 units
6. "Event Staff Totes" — 120 units

Add a note: `"📸 More work on Instagram — @trashysteez"` (placeholder — they can update handle)

### 4.7 FOR COMPANIES

Section title: `"PRINTING FOR YOUR BRAND"` in Bebas Neue.
Subtitle: `"From 10 to 10,000 units — we handle campaigns of any size."`

Two-column layout (stack on mobile):

**Left column — What we offer companies:**
- Branded campaign merchandise
- Staff uniforms & workwear
- Event giveaways & activations
- Retail-ready product lines
- Corporate gifting packages

**Right column — Campaign enquiry form:**
```
Company name:    [text input]
Your name:       [text input]  
Phone/WhatsApp:  [tel input]
What do you need? [textarea]
Estimated qty:   [select: 10-50 / 50-200 / 200-500 / 500+]
[SEND VIA WHATSAPP button]
```
The form's "SEND VIA WHATSAPP" button collects the form data and opens WhatsApp with the enquiry pre-filled:
```
Hi Trashy Steez! I'm reaching out about a company order:

Company: [company]
Contact: [name]
Phone: [phone]
Requirements: [textarea]
Estimated quantity: [qty range]
```

### 4.8 TRUST STRIP

A horizontal scrolling strip (or static grid on desktop) showing:
- `500+ CAMPAIGNS PRINTED` 
- `NATIONWIDE DELIVERY`
- `FAST TURNAROUND`
- `CUSTOM DESIGNS WELCOME`
- `SA OWNED & OPERATED`

Each stat in Bebas Neue (large number) + DM Sans description. Use a subtle CSS marquee/scroll animation on mobile if desired.

Also add 2–3 placeholder testimonial cards:
> *"Fast, high quality, and the team was super helpful. Our staff shirts looked incredible."*  
> — **Marketing Manager, Johannesburg**

> *"We've used Trashy Steez for 3 campaigns now. Always on time and always on point."*  
> — **Brand Coordinator, Cape Town**

### 4.9 CONTACT

Simple, uncluttered contact section. **No big slogan headline.** Just a clean contact block.

**Layout:**
- Small section label in Space Mono (cyan, 11px): `// GET IN TOUCH`
- One line in Bebas Neue (`clamp(36px, 5vw, 64px)`), white: `LET'S TALK`
- Short body text in DM Sans: `"Drop us a message on WhatsApp or email — we respond quickly."`
- Large WhatsApp button (primary, glowing cyan — biggest CTA on the page)
- Below the button, three small contact detail lines:
  - `+27 68 057 0848`
  - `[placeholder@trashysteez.co.za]`
  - `South Africa — nationwide delivery`
- Instagram handle: `@trashysteez` (placeholder)

### 4.10 FOOTER

Minimal dark footer:
- Logo (small) left
- `© 2025 Trashy Steez Prints. All rights reserved.`
- Links: Products | Quote | Portfolio | Contact
- "Made in South Africa 🇿🇦"

---

## 5. FLOATING WHATSAPP BUTTON

**Always visible**, fixed to bottom-right corner:

```css
.whatsapp-float {
  position: fixed;
  bottom: 24px;
  right: 24px;
  z-index: 999;
  width: 60px;
  height: 60px;
  background: #25D366;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 20px rgba(37, 211, 102, 0.5);
  cursor: pointer;
  transition: transform 0.2s ease-out, box-shadow 0.2s ease-out;
}
.whatsapp-float:hover {
  transform: scale(1.1);
  box-shadow: 0 4px 30px rgba(37, 211, 102, 0.7);
}
```

Use the WhatsApp SVG icon inside it. On click, opens:
`https://wa.me/27680570848?text=Hi%20Trashy%20Steez!%20I%27d%20like%20to%20get%20a%20quote.`

Add a small pulsing notification dot (CSS animation) on the button to draw attention.

---

## 6. ANIMATIONS & MOTION

Follow these performance rules strictly:

- **Only animate `transform` and `opacity`** — never `width`, `height`, `top`, `left`, `margin`, or `padding`
- **Scroll reveals**: Use `IntersectionObserver` (never raw scroll listeners) to add `.visible` class
- **Hover effects**: Gate with `@media (hover: hover) and (pointer: fine)`
- **Duration limits**: Micro-interactions 100ms, standard transitions 200–300ms, hero loads 300–400ms, total stagger sequence ≤ 800ms
- **Always include**:
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

**Specific animations to implement:**

1. **Hero entrance**: Staggered fade-up for label → headline line 1 → headline line 2 → subtext → buttons. Delays: 0, 100ms, 200ms, 350ms, 500ms.
2. **Section reveals**: All sections use `.fade-up` class, triggered by IntersectionObserver at `threshold: 0.15`
3. **Product card hover**: `translateY(-6px)` + border brightens, 200ms ease-out
4. **Quote wizard step transitions**: Slide left/right using `translateX` + `opacity`
5. **WhatsApp button pulse**: CSS `@keyframes pulse` on the notification dot (scale 1 → 1.4, infinite, 1.5s)
6. **Navbar**: Adds `.scrolled` class after 50px scroll — tightens padding slightly

---

## 7. MOBILE REQUIREMENTS

Build **mobile-first**. Base styles at 375px, enhance upward.

```css
/* Mobile base */
.container { padding: 16px; }

/* Tablet */
@media (min-width: 768px) { .container { padding: 24px; } }

/* Desktop */
@media (min-width: 1024px) { .container { max-width: 1280px; margin: 0 auto; padding: 0 48px; } }
```

Mobile-specific requirements:
- Hamburger nav (full-screen overlay, large tap targets ≥ 44×44px)
- Quote wizard steps are single-column, form inputs full-width
- Product grid: 1 column on mobile, 2 on tablet, 3 on desktop
- Portfolio grid: 1 column on mobile, 2 on tablet, 3 on desktop
- How it works: vertical steps (not horizontal)
- All font inputs `font-size: 16px` minimum (prevents iOS zoom)
- Hero headline uses `clamp()` to scale gracefully
- WhatsApp float button always reachable (not covered by other elements)
- Sticky "GET QUOTE" bar at bottom of mobile viewport on hero section (disappears once user scrolls past hero)

---

## 8. TECHNICAL REQUIREMENTS

- **Single file preferred**: `index.html` with embedded `<style>` and `<script>` blocks, OR split into `index.html` + `style.css` + `script.js`
- **No framework required** — vanilla HTML/CSS/JS only
- **Google Fonts** via `<link>` tag in `<head>`
- **WhatsApp SVG icon** — inline SVG or from a CDN
- **Viewport meta**: `<meta name="viewport" content="width=device-width, initial-scale=1">`
- **Meta description**: `"Trashy Steez Prints — South Africa's boldest custom print studio. T-shirts, hoodies, caps, bottles & more. Get an instant quote online."`
- **Smooth scroll**: `html { scroll-behavior: smooth; }` + override with `prefers-reduced-motion`
- **Quote wizard state**: Managed entirely in JS (no localStorage needed — fresh each session)
- **Form submissions**: Both forms open WhatsApp (no backend required)
- **Image placeholders**: Use styled `<div>` placeholders with aspect-ratio set, coloured in `var(--color-surface-2)` with a subtle `[PHOTO]` label. These are easy for the client to swap out.

---

## 9. COPY & CONTENT REFERENCE

### Taglines (use throughout)
- `"WE MAKE YOUR BRAND LOUD."`
- `"PRINT BOLD. STAND OUT."`
- `"YOUR DESIGN. OUR OBSESSION."`
- `"FROM CONCEPT TO CAMPAIGN."`

### Company value props
- Fast turnaround
- Nationwide delivery across South Africa
- Bulk pricing that makes sense
- No artwork? We can help create it
- WhatsApp-first — quick responses, no corporate fluff

### Section subheadings
- Products: `"We print on everything."`
- Quote: `"No calls. No waiting. Just your price."`
- Portfolio: `"Campaigns we've brought to life."`
- Companies: `"From 10 to 10,000 units."`
- Contact: `"Let's Talk"` + `"Drop us a message on WhatsApp or email — we respond quickly."`

---

## 10. DELIVERABLE CHECKLIST

Before considering it done, verify:

- [ ] All 8 sections render correctly at 375px width, no horizontal scroll
- [ ] Quote wizard completes all 4 steps and generates a WhatsApp link
- [ ] WhatsApp float button works and opens correct number
- [ ] Hamburger nav opens/closes on mobile
- [ ] All product cards scroll to #quote with product pre-selected
- [ ] Company enquiry form generates WhatsApp message
- [ ] All animations use only `transform` / `opacity`
- [ ] `prefers-reduced-motion` respected
- [ ] IntersectionObserver scroll reveals work
- [ ] Fonts load correctly (Bebas Neue, DM Sans, Space Mono)
- [ ] Neon glow effects on hero, CTAs, and wizard active step
- [ ] Background grid animation in hero (CSS only, subtle)
- [ ] Page loads fast — no render-blocking JS, fonts use `display=swap`
- [ ] Meta description and viewport meta present

---

---

## 11. IMAGE ASSETS — All files in project folder

### Real photos (primary assets — these drive the site)

| File | Section | How to use |
|------|---------|------------|
| `photo-factory.jpg` | `#hero` | Full-bleed hero background — the MONEY SHOT. Aerial view of industrial screen printing carousel machines. Cyan color-grade overlay via `::after`. See Section 4.2 for exact CSS. |
| `photo-workshop.jpg` | `#behind-the-print` | Left-column of 2-column split section. Desaturated slightly, right-edge gradient fade into dark background. See Section 4.5. |
| `IMG_0926.jpg` | Navbar + Footer | The Trashy Steez logo (circular neon badge). Use as `<img>` with `border-radius: 50%`, height 48px in nav. |

### AI-generated texture backgrounds (supporting assets)

| File | Section | Effect |
|------|---------|--------|
| `bg-quote.jpg` | `#how-it-works` + `#quote` | Plasma wave texture. Use with 80% dark overlay. |
| `bg-portfolio.jpg` | `#portfolio` | Neon bokeh/star field. Use with 80% dark overlay. |

### CSS for real photo sections

```css
/* ── HERO — factory aerial ── */
#hero {
  background-image: url('photo-factory.jpg');
  background-size: cover;
  background-position: center top;
  position: relative; min-height: 100vh;
}
#hero::before {  /* dark gradient overlay */
  content: ''; position: absolute; inset: 0; z-index: 1;
  background: linear-gradient(to bottom,
    rgba(5,9,26,0.70) 0%, rgba(5,9,26,0.50) 50%, rgba(5,9,26,0.88) 100%);
}
#hero::after {  /* cyan color-grade tint */
  content: ''; position: absolute; inset: 0; z-index: 2;
  background: rgba(0,60,100,0.20); mix-blend-mode: color;
}
#hero > * { position: relative; z-index: 3; }

/* ── WORKSHOP SPLIT — sewing room ── */
.workshop-photo {
  width: 100%; height: 100%; min-height: 560px;
  object-fit: cover; object-position: center;
  filter: brightness(0.75) contrast(1.05) saturate(0.65);
}

/* ── TEXTURE SECTIONS ── */
#quote, #how-it-works {
  background-image: url('bg-quote.jpg');
  background-size: cover; background-position: center;
  position: relative;
}
#quote::before, #how-it-works::before {
  content: ''; position: absolute; inset: 0;
  background: rgba(5,9,26,0.80); z-index: 0;
}
#quote > *, #how-it-works > * { position: relative; z-index: 1; }

#portfolio {
  background-image: url('bg-portfolio.jpg');
  background-size: cover; background-position: center;
  position: relative;
}
#portfolio::before {
  content: ''; position: absolute; inset: 0;
  background: rgba(5,9,26,0.80); z-index: 0;
}
#portfolio > * { position: relative; z-index: 1; }
```

**Mobile note:** Disable `background-attachment: fixed` on mobile (iOS doesn't support it):
```css
@media (max-width: 767px) {
  #hero, #quote, #portfolio { background-attachment: scroll; }
}
```

---

## 12. UI/UX DESIGN DETAILS (from frontend-design skill)

These are the details that separate a memorable site from a generic one. Implement all of these.

### Grain overlay (global — apply to entire page)
```html
<div class="grain-overlay" aria-hidden="true"></div>
```
```css
.grain-overlay {
  position: fixed; inset: 0; z-index: 9999; pointer-events: none;
  opacity: 0.04;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  background-size: 200px;
}
```
This subtle noise texture makes everything feel tactile and printed — not digital and sterile.

### Typography — "LOUD." treatment
The word `LOUD.` in the hero must be on its own line, much larger than the rest, full cyan, with the strong glow:
```css
.hero-loud {
  display: block;
  color: var(--color-cyan);
  text-shadow: var(--glow-cyan-strong);
  font-size: clamp(100px, 18vw, 200px);
  line-height: 0.9;
  letter-spacing: -0.02em;
}
```

### Product cards — staggered "laid out" feel
Cards are not in a perfect grid. Alternate cards have a slight rotation and vertical offset to feel like physical items on a table:
```css
.product-card:nth-child(odd)  { transform: rotate(-0.8deg) translateY(4px); }
.product-card:nth-child(even) { transform: rotate(0.6deg)  translateY(-4px); }
.product-card:hover            { transform: rotate(0deg) translateY(-8px) scale(1.02); 
                                  border-color: var(--color-cyan);
                                  box-shadow: var(--glow-cyan); }
/* All transitions: transform + box-shadow only, 200ms ease-out */
```

### Quote wizard — styled as a work order / print ticket
The wizard container should feel like a real printed form — industrial, authentic:
```css
.quote-wizard {
  border: 1px dashed rgba(0,212,255,0.3);
  position: relative;
}
.quote-wizard::before {
  content: 'WORK ORDER #' attr(data-order-id);
  position: absolute; top: -12px; left: 24px;
  font-family: 'Space Mono', monospace;
  font-size: 11px; color: var(--color-cyan);
  background: var(--color-bg); padding: 0 8px;
  letter-spacing: 0.1em;
}
```
Generate a random order number on page load: `Math.floor(Math.random() * 9000) + 1000`

### Horizontal marquee stat strip
Between the hero and products sections, add a full-width scrolling marquee:
```html
<div class="marquee-strip" aria-label="Company highlights">
  <div class="marquee-track">
    <span>500+ CAMPAIGNS PRINTED</span>
    <span class="dot" aria-hidden="true">✦</span>
    <span>NATIONWIDE DELIVERY</span>
    <span class="dot" aria-hidden="true">✦</span>
    <span>IN-HOUSE PRODUCTION</span>
    <span class="dot" aria-hidden="true">✦</span>
    <span>FAST TURNAROUND</span>
    <span class="dot" aria-hidden="true">✦</span>
    <span>CUSTOM DESIGNS WELCOME</span>
    <span class="dot" aria-hidden="true">✦</span>
    <!-- duplicate for seamless loop -->
  </div>
</div>
```
```css
.marquee-strip {
  background: var(--color-cyan); color: var(--color-bg);
  overflow: hidden; white-space: nowrap; padding: 14px 0;
}
.marquee-track {
  display: inline-block;
  font-family: 'Bebas Neue', sans-serif;
  font-size: 18px; letter-spacing: 0.08em;
  animation: marquee 25s linear infinite;
}
@keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }
.dot { color: rgba(5,9,26,0.5); margin: 0 24px; }
@media (prefers-reduced-motion: reduce) { .marquee-track { animation: none; } }
```

### Section transition — "printing press" feel
As each section enters on scroll, it should feel like it's being printed from the bottom up. Use this IntersectionObserver class:
```css
.print-in {
  opacity: 0;
  transform: translateY(32px) skewY(0.5deg); /* slight skew = paper coming off press */
  transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}
.print-in.visible {
  opacity: 1;
  transform: translateY(0) skewY(0);
}
```
Apply `.print-in` to every section heading, card grid, and major content block.

### Stat numbers — animated count-up
The stat numbers in the "Behind the Print" section (500+, 48hr, 100%) should count up when scrolled into view:
```js
function animateCount(el, target, suffix = '') {
  let start = 0;
  const duration = 1500;
  const step = (timestamp) => {
    if (!start) start = timestamp;
    const progress = Math.min((timestamp - start) / duration, 1);
    el.textContent = Math.floor(progress * target) + suffix;
    if (progress < 1) requestAnimationFrame(step);
  };
  requestAnimationFrame(step);
}
// Trigger via IntersectionObserver when .stat-number enters viewport
```

### Custom cursor (desktop only)
A small cyan crosshair cursor that reinforces the precision/printing theme:
```css
@media (hover: hover) and (pointer: fine) {
  body { cursor: none; }
  .cursor {
    position: fixed; width: 20px; height: 20px; z-index: 99999;
    pointer-events: none; mix-blend-mode: difference;
    border: 1.5px solid var(--color-cyan); border-radius: 50%;
    transform: translate(-50%, -50%);
    transition: transform 0.1s ease-out, width 0.2s, height 0.2s;
  }
  .cursor.hovering { width: 40px; height: 40px; background: rgba(0,212,255,0.1); }
}
```
```js
const cursor = document.querySelector('.cursor');
document.addEventListener('mousemove', e => {
  cursor.style.left = e.clientX + 'px';
  cursor.style.top  = e.clientY + 'px';
});
document.querySelectorAll('a, button').forEach(el => {
  el.addEventListener('mouseenter', () => cursor.classList.add('hovering'));
  el.addEventListener('mouseleave', () => cursor.classList.remove('hovering'));
});
```

---

## 13. SUPABASE INTEGRATION

The site uses **Supabase** as a lightweight backend to log quote requests and company enquiries. No auth needed — anonymous inserts only.

### Setup

1. Go to your Supabase project → SQL Editor → run this to create the tables:

```sql
-- Quote requests from the wizard
CREATE TABLE quote_requests (
  id          uuid DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at  timestamptz DEFAULT now(),
  product     text NOT NULL,
  quantity    int NOT NULL,
  print_method text NOT NULL,
  est_low     int,
  est_high    int
);

-- Company enquiries from the B2B form
CREATE TABLE company_enquiries (
  id           uuid DEFAULT gen_random_uuid() PRIMARY KEY,
  created_at   timestamptz DEFAULT now(),
  company_name text,
  contact_name text,
  phone        text,
  requirements text,
  qty_range    text
);

-- Enable Row Level Security but allow anonymous inserts
ALTER TABLE quote_requests    ENABLE ROW LEVEL SECURITY;
ALTER TABLE company_enquiries ENABLE ROW LEVEL SECURITY;

CREATE POLICY "allow anon insert" ON quote_requests    FOR INSERT TO anon WITH CHECK (true);
CREATE POLICY "allow anon insert" ON company_enquiries FOR INSERT TO anon WITH CHECK (true);
```

2. Get your **Supabase project URL** and **anon public key** from Project Settings → API.

3. Add the Supabase JS client via CDN in `<head>`:
```html
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2/dist/umd/supabase.min.js"></script>
```

4. Initialise in your script (replace placeholders):
```js
const SUPABASE_URL  = 'https://YOUR_PROJECT_ID.supabase.co';
const SUPABASE_KEY  = 'YOUR_ANON_PUBLIC_KEY';
const db = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);
```

### Where to call Supabase

**On quote wizard Step 4 (when user sees their estimate):**
```js
async function logQuoteRequest(product, quantity, method, estLow, estHigh) {
  await db.from('quote_requests').insert({
    product, quantity, print_method: method, est_low: estLow, est_high: estHigh
  });
}
// Call this before showing the WhatsApp button on Step 4
```

**On company enquiry form submit:**
```js
async function logCompanyEnquiry(data) {
  await db.from('company_enquiries').insert({
    company_name: data.company,
    contact_name: data.name,
    phone: data.phone,
    requirements: data.requirements,
    qty_range: data.qtyRange
  });
}
// Call this before opening the WhatsApp link
```

Both calls are fire-and-forget (don't block the WhatsApp handoff). Wrap in try/catch and silently ignore errors — the user must never see a Supabase error; the WhatsApp link always opens regardless.

```js
try { await logQuoteRequest(...); } catch(e) { /* silent */ }
// then open WhatsApp
```

---

## 14. GITHUB + VERCEL DEPLOYMENT

### Git setup (run once in your project folder)

```bash
git init
git add .
git commit -m "feat: initial Trashy Steez Prints build"
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/trashy-steez-website.git
git branch -M main
git push -u origin main
```

> **Replace `YOUR_GITHUB_USERNAME`** with the actual GitHub username before running.

### .gitignore (create this file)

```
.env
.env.local
node_modules/
.DS_Store
*.log
```

### Vercel deployment

1. Go to [vercel.com](https://vercel.com) → **Add New Project** → import the GitHub repo `trashy-steez-website`
2. Framework preset: **Other** (it's a static HTML site)
3. Build command: leave blank (no build step)
4. Output directory: `.` (root)
5. Click **Deploy** — Vercel auto-deploys on every push to `main`

### Environment variables on Vercel

Add these in Vercel Project Settings → Environment Variables:
```
SUPABASE_URL   =  https://YOUR_PROJECT_ID.supabase.co
SUPABASE_KEY   =  YOUR_ANON_PUBLIC_KEY
```

Then in your `index.html`, reference them. Since this is a static site (no build step), **embed the values directly** in the script — the anon key is safe to expose publicly (it's designed for this). Do NOT use the service role key.

### Push workflow after changes

```bash
git add .
git commit -m "fix: [describe what you changed]"
git push
# Vercel auto-deploys within ~30 seconds
```

### Custom domain (optional)

In Vercel Project → Settings → Domains → add `trashysteezprints.co.za` (or whatever domain they have). Point the DNS A record to Vercel's IP — Vercel provides the exact records to add.

---

*End of brief. Paste everything above into Claude Code and it has everything it needs to build Trashy Steez Prints from scratch — backgrounds, Supabase logging, GitHub repo, and Vercel deployment all included.*
