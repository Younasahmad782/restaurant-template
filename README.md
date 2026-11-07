# Premium Bilingual Restaurant Website — Customisation Guide

**Developed by Muhammad Younus** — Web Developer · [Portfolio](https://younasahmad782.github.io/portfolio/)

A complete, single-file restaurant website template: **Arabic (default, RTL) + English (LTR)**,
instant in-page language toggle, digital menu with category filters, WhatsApp ordering,
gallery lightbox, offers, reviews, contact + Google Maps, floating WhatsApp button.

**File:** `index.html` — everything (HTML + CSS + JS) is in this one file. No build step.

## Preview it

Double-click `index.html` in any browser, or serve the folder:

```bash
cd restaurant-template
python3 -m http.server 8000
# open http://127.0.0.1:8000
```

## Customise it — everything is in the CONFIG object

Open `index.html`, scroll to the bottom `<script>`, and edit **only** the `CONFIG` object.
Every field is commented. Nothing else in the file needs to change.

| CONFIG field | What it changes |
|---|---|
| `name` | Restaurant name (AR + EN) — header, footer, page title |
| `tagline` | Short line under the name |
| `phoneDisplay` / `phoneLink` | Phone number shown / dialled — currently the owner's number **+92 345 7305226** (set 2026-11-06). Replace with the restaurant's own number when customising for a client |
| `whatsapp` | **The owner's number +92 345 7305226 is already in place** (digits only with country code, no `+`). Drives the floating button, every Order button and the contact WhatsApp link. Replace with the restaurant's own WhatsApp number when customising for a client |
| `address` / `hours` | Contact section + footer (AR + EN) |
| `mapQuery` | Google Maps embed location (also update the "Get Directions" link in the HTML) |
| `categories` | Menu categories — add, rename or remove freely (each needs `id`, `ar`, `en`) |
| `menu` | Every dish: category `cat`, `price` (SAR), `img`, `name` + `desc` (AR + EN), `popular` badge, `sample` badge |
| `offers` | The 3 offer cards: tag, price, old price (`was`), image, title + description |
| `why` | The 4 feature cards (icon: `leaf` / `star` / `bell` / `home`) |
| `gallery` | 8 photos + captions (AR + EN) |
| `reviews` | Sample reviews — replace with real ones (see below) |

Static text (nav, hero, section titles, buttons, footer) lives in the `I18N` object
right below CONFIG — `ar:` and `en:` for every string.

### Colours

CSS variables at the top of the `<style>` block:

```css
--green:#16382a;   /* deep forest green (primary) */
--gold:#c9a227;    /* warm gold (secondary) */
--cream:#faf6ee;   /* warm cream background */
--charcoal:#23272b;/* text */
```

Change the four values and the whole site re-themes.

### Images

Dish/gallery photos are Unsplash URLs (`images.unsplash.com/...`). To use the
restaurant's own photos, replace any `img:` value with a local path
(e.g. `images/mandi.jpg`) and put the file next to `index.html`.

### Language behaviour

- Default language: **Arabic, RTL**. Toggle in the header switches instantly
  (no reload), flips the whole layout to LTR for English, and remembers the
  choice (`localStorage`) across visits.
- On phones under 480 px the toggle shows only the language you can switch
  *to*, so the header never crowds.
- Fonts: Cairo + Tajawal (Arabic), Playfair Display + Poppins (English),
  loaded from Google Fonts. If the restaurant is offline-first, self-host
  the fonts and point the site at them.

## Sample content — replace before showing a client as "live"

The demo brand is **مطعم الذواقة / Althawaqa Restaurant**. The owner's phone
**+92 345 7305226** is already in the template as the phone + WhatsApp number
(set 2026-11-06), so demo orders and enquiries reach him — replace it with the
real restaurant's number when customising for a client. Everything else sample
is marked on the page:

- Every menu dish and offer carries a small **"عينة / Sample"** badge
  (remove it by setting `sample: false` on that item).
- Reviews are labelled **"Sample review — replace with real customer reviews"**
  and carry a Sample tag. **Never present them as genuine feedback** — replace
  with real customer names, words and star ratings.
- The About text, offers and prices are demo copy — rewrite for the real
  restaurant. No real restaurant's facts were invented here; all of it is
  clearly-marked placeholder content.

## How ordering works

There is no backend and no cart. Each dish's **Order** button opens WhatsApp
with a pre-filled message ("Hello, I would like to order: Meat Mandi — 45 SAR"
in the current language). The floating WhatsApp button and the contact section
open a general enquiry chat. If a restaurant wants online payment or a cart,
that is a separate build.

## Deploy it

- **GitHub Pages:** create a repo, upload `index.html`, Settings → Pages → deploy from main. Free.
- **Netlify / Vercel:** drag the folder into the dashboard. Free tier, no card.
- **Any shared hosting:** upload `index.html` to `public_html`.

## Verified (2026-11-06)

- **51/51 automated checks green** (Playwright, local render): default AR/RTL,
  toggle to EN/LTR and back, language persists after reload, 19 menu cards,
  filters (grilled = 2, beverages = 3), lightbox open/next/Esc-close, WhatsApp
  `wa.me` links with the right number + pre-filled dish, call link, map embed,
  mobile drawer open/close, **no horizontal overflow at 320–1920 px in both
  languages**, no JS errors.
- All 30 Unsplash photo URLs return HTTP 200 (checked with curl).
- Screenshots in `screenshots/` (Arabic + English, desktop + mobile) were
  rendered from the real file with real photos and fonts.

One known environment limit: the Google Maps embed needs internet in the
visitor's browser (normal for any site). It was verified by code, not by a
live map render in the test VM.
