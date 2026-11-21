# Bhavana & Mukund — PADHARO · The Royal Gateway (v8)

A mobile-first (9:16) scroll-driven Jaipur wedding invitation in one folder.
Open `index.html` in any modern browser, or deploy the whole folder to
Vercel (steps below) — any static host works, no build step.

## What is inside

```
index.html            the whole site (CSS + JS inline)
images/
  gate.webp           the real Peacock Gate photo (2752×1536) — the two carved
                      door leaves are sliced from these exact pixels and swing
                      open in 3D when tapped
  palace-sunset.webp  sunset palace re-exported in v7 from the supplied
                      2752×1536 master PNG (no upscaling, no sharpening) —
                      seen through the open doorway AND the hero arch zoom
  couple-portrait.webp  the couple's marigold-swing portrait
  doli.webp             golden doli — rides the timeline thread
  mandala.webp          blue peacock mandala plate (wheels + medallions)
  desert.webp           desert village panorama (closing)
  ganesha-mark.webp     golden Ganesha mandala (gate doorway + hero crown)
  logo-mark.webp        MB monogram emblem (nav, hero palace, RSVP seal)
  logo-full.webp        monogram emblem on the scratch-card reveal
  photo-01..11.webp     the couple's 11 photos (1400px, q80)
  og-cover.jpg          WhatsApp / social preview card (1200x630)
audio:
  mangal-rang.mp3       "Mangal Rang Hai Prem Ke Rango Ka Sangam"
                        (begins once the doors stand open; mute button in the nav)
```

## What changed in v8 (this pass)

- **Hero emblems aligned.** The golden Ganesha mandala now crowns the hero
  ABOVE the "Shubh Vivah" text (with a soft dark halo so it reads crisply
  against the sunset), and the MB monogram sits at the centre of the palace
  facade below the text — nothing merges with the names any more.
- **Scratch card sealed properly.** The date text used to paint ABOVE the
  foil (a z-index slip), so "18 JANUARY 2027" was readable before
  scratching. The foil now fully covers the card; scratching (or Tap to
  reveal) uncovers the monogram at the TOP with the date lines BELOW it.
- **Baraat & Varmala split inside the same card**: BARAAT NIKASI · 4:30 PM
  and VARMALA · 5:30 PM listed separately (side strip now says
  "Day Two · 4:30 pm onwards"). The Add-to-calendar button downloads BOTH
  events (two VEVENTs in one .ics; Android opens Baraat Nikasi pre-filled).
- **Add-to-calendar dates fixed** — the old date string was invalid
  (`2027-01-18T163000:00`), so every generated invite carried NaN
  timestamps. All 7 events now land at their real IST times.
- **बत्तीसी** — the Hindi spelling on the Battisi card is corrected.
- **Gallery revolves on its own.** A twin of every photo rides behind the
  strip, so it auto-advances every ~3.8 s in an endless, seamless loop
  (no visible rewind). It pauses the moment you touch, hover, arrow, open
  the lightbox or leave the section, and drifts on ~7 s later.
- **New gallery photo**: "Our First Jyotirling Darshan" (the temple selfie,
  photo-11) — 10 photos in the strip now.
- Verified at 360 / 393 / 1440 px, light + dark: zero console errors,
  scratch sealed before the reveal, seamless loop wrap-around tested.

## What changed in v7 (the final polish pass)

- **The scratch card never self-reveals again.** It always loads covered in
  foil; only an actual scratch (or the Tap to reveal button) uncovers the
  date. The "remember the reveal on this device" behaviour is gone — that
  is what made the date appear already-revealed on reload.
- **"With the blessings of our elders" line removed** from The Couple header
  (it now goes straight to the heading, like the other sections).
- **No times in the venue card** — just ADDRESS and DATE (the festivities
  cards still carry their own times; the calendar invites do too).
- **The RSVP "select events" checkbox grid is gone** — from the form, the
  CSS, the WhatsApp message and the sheet payload (replies are now name /
  attending / guests / notes).
- **पधारो lost its letter-gaps.** Devanagari never takes letter-spacing —
  the gate line, the invocation and the closing credit now render with the
  letters joined properly (a touch larger to compensate).
- **"~ with love Mukund Ratha"** signs the invite at the bottom-right of the
  page, under the पधारो credit, in the same Great Vibes script.
- **Palace sharpness, for real this time**: `palace-sunset.webp` is exported
  straight from the supplied 2752×1536 master PNG (q88, 682 KB) — no 1.5×
  fake upscale, no over-sharpening halos. Verified crisp at 1×–1.72× on
  phones and desktop.
- Verified end-to-end on 393×852 (dpr 3) and 1280×800: doors reach ±106°,
  music starts only once the doors stand open (~1.6 s after the tap), the
  step-through glides into the hero, and petals are untouched.

## What changed in v6 (the "gate rebuild" pass)

- **The Guest Guide / "Plan your stay" section is gone** — the contact
  buttons (WhatsApp + call Vasudev Toshniwal · +91 98865 39444) live on in
  the closing section, so nothing was lost.
- **The gate is the real peacock-gate photo**, full-bleed on every screen.
  The two carved door leaves are cut from the photo's own door pixels
  (measured on the image: seam, arch apex and spring points), so closed
  doors are invisible — then they swing past 90° in 3D and vanish cleanly
  (no more "half-open" look).
- **A real doorway reveal**: the doors open onto a shadowed, lantern-lit
  passage with the sunset palace glowing beyond it — depth shading, jamb
  shadow and floor light, not a flat panel.
- **Music starts only after the doors stand open** (1.5 s after the tap),
  never before.
- **The step-through**: once the doors are open the camera dives into the
  doorway (2.05× zoom into the arch) under a warm flood of light while an
  eased 1.25 s glide carries you into the hero — which continues from the
  SAME palace photo, so the journey reads as one walk through the gate.
  The glide is now smooth on phones too (it used to jump-cut on touch
  devices); any touch or wheel hands control straight back to you.
- **Palace sharpness**: the hero source is re-exported at 4128×2304
  (1.5× Lanczos + gentle unsharp) and the arch zoom now ends at 1.72×
  (was 2.2×) with the cream flare arriving a touch earlier — crisp at
  1×–1.7× on retina phones and 1440p desktops, no pixelation.
- The preloader now waits for the gate photo to decode (max 2.6 s) so the
  first frame is never an empty dark screen.
- Falling petals, event cards, gallery, RSVP and wishes are untouched
  from v5.

## What changed in v5 (the "make it world-class" pass)

**Feel & motion**
- Petals now drift at one calm, constant speed — a single requestAnimationFrame loop replaces the old wake/tick guard, which let every scroll event spawn an extra animation chain (that is why petals sped up while scrolling).
- Section background colours are driven by IntersectionObserver with a 1s CSS crossfade — no more per-frame colour writes, so scrolling no longer stutters when the page turns midnight at Sangeet.
- The two blue porcelain wheels now turn slowly (130s per rotation) at low opacity, blended behind the content (z-index 0, hidden from taps; disabled for reduced-motion users).
- Sangeet glitter is drawn from two cached sprites instead of a radial gradient per particle per frame.

**Sections**
- The first "Save the days" date window is gone — the countdown + scratch-to-reveal card is the single date reveal.
- The Couple section drops the illustrated jharokha composites: one grand marigold-swing portrait in an arch frame, plus two name plaques with the parents' lines.
- The MYRAH card glitch is fixed — the missing stage CSS made five illustrations stack into a giant column. The shagun tray, envelopes and dupatta wave are now one composed scene.
- The Gallery is a clean film strip of arch-framed photos (swipe or arrows, tap for lightbox) instead of the 3D coverflow.
- Colour themes live inside the Sangeet and Haldi event cards now — the separate "What to wear" guide entry is removed.
- Contact adds Vasudev Toshniwal · +91 98865 39444 (call button) beside the WhatsApp link, in the guide and the closing.

**Image quality & weight**
- The palace hero zoom ends at 2.2x (was 4.8x) over a 1.5x Lanczos-upscaled, re-sharpened source — no pixelation; a light flare enters as you reach the arch.
- Every artwork is WebP with alpha, photos are 1400px WebP q80. First load ≈ 1.6 MB (was ~9.6 MB), full page ≈ 4.1 MB (was ~15 MB). Below-fold images hydrate via IntersectionObserver (data-src), so the preloader cannot pull them early.
- Dark mode: light event cards set their own dark ink, so text stays readable (was ~1.4:1). Eyebrows on dark cards meet 4.5:1.
- Tested at 320 / 360 / 393 / 412 / 768 / 1440 px, light and dark, plus reduced-motion: zero console errors, no horizontal scroll.

## What changed in v4 (the "make it proper" pass)

- **No more white boxes**: every decorative artwork is now a real
  transparent PNG cutout (jharokha frame, golden doli, brass gallery
  frame, mandala plate) — they float cleanly on the page, in light AND
  dark mode.
- **No webp anywhere**: artwork is PNG, photos are your original JPGs
  copied untouched (zero recompression). The palace was regenerated at
  1536x2688 — the old one was upscaled from a 286px file and looked
  pixelated.
- **Events returned to the previous-version design**: themed cloth
  cards (cream Battisi, gold Myrah, midnight Sangeet with reactive
  glitter + disco ball, pastel Haldi with a marigold garland and
  tap-to-burst petals, crimson Baraat with varmala rings, indigo
  Reception with stars + chandelier). No scroll artwork. The golden
  doli still travels the thread.
- **Couple section**: now exactly two cards — groom and bride — with
  the royal portraits embedded in the jharokha window and the parents'
  names directly below (the separate family section is gone).
- **Add to calendar fixed on phones**: on Android it now opens Google
  Calendar with the event pre-filled (no stray .ics download); iPhone
  and desktop keep the .ics.
- **Petals slowed down** (~4x slower, fewer, softer) — no more
  "glitching" feel.
- Removed the duplicate Ganesha line (hero keeps "Shubh Vivah"; the
  invocation stays in the invitation section) and other doubled bits.
- Fixed the name typo (MUKUND TOSHNIWAL).

## What changed in v3 (the PADHARO mobile-first edition)

The site was rebuilt around the reference video, portrait (9:16) first:

- **New gate**: the real peacock-gateway artwork with the wooden double
  doors sliced out of the same image — tapping (or scrolling) swings them
  open in 3D (`rotateY(±82°)`), the music starts, and you glide into the hero.
- **New hero**: the sunset-palace artwork; the names sit in the evening sky
  and scrolling zooms through the palace archway (scale 1 → 4.8) into the
  cream parchment body.
- **Jharokha cards** with sliding jaali shutters open on scroll: the date
  plaque, the three royal portrait cards (groom / couple / bride) and the
  two family shells (emerald = groom's, lotus-pink = bride's).
- **Festivities**: each event is a crimson *farman* scroll that unrolls on
  scroll, with its ceremony icon; the golden doli travels down the thread
  as you scroll. Desktop keeps the three-column timeline
  (date · golden thread · scroll), cards alternating sides.
- **Gallery**: the real photos now sit inside brass arch frames on an
  infinite 3D coverflow (neighbours on both edges), arch-shaped pagination
  dots, and a tap-to-zoom lightbox.
- **New spec SVGs** rendered inline: rotating blue peacock-mandala wheels,
  six ceremony icons (kalash, manjeera, dhol, urli, agni, chhatri),
  crimson ribbon banners, the vintage venue map, and the M&B gold wax seal
  on the RSVP card.
- Closing sign-off over the desert caravan panorama; hashtag
  **#MukundKiBhavana** now live in the hero, the closing and the share text.
- Countdown runs to the wedding evening (18 Jan 2027, 7:00 pm IST);
  scratch card reveals at 42% with a gold/crimson confetti burst.
- Verified at 360/393/412/768/1440 px: no horizontal scroll, zero console
  errors, dark scheme + reduced-motion + low-end tiers all handled.

## Edit me — the CONFIG block (top of the script in index.html)

| Key | Meaning | While empty |
|---|---|---|
| `GROOM.grand` / `BRIDE.grand` | "Grandson/Granddaughter of …" line above the parents' line | the line hides itself |
| `GROOM.parents` / `BRIDE.parents` | "Son/Daughter of …" lines under the portrait cards | the line hides itself |
| `MUSIC_SRC` | currently `audio/mangal-rang.mp3` | music toggle hidden |
| `PHOTO_GALLERY_URL` | Kamero / PicsDrop gallery link (Memories QR) | section hidden |
| `HASHTAG` | `#MukundKiBhavana` — hero chip + closing + share text | hidden |
| `RSVP_ENDPOINT` | Google Apps Script web-app URL or Formspree ID | WhatsApp message flow |
| `WISHES_ENDPOINT` | separate URL; empty = **reuse `RSVP_ENDPOINT`** (one sheet, `type` column splits rows) | this-device wish wall |
| `WHATSAPP_URL` | `wa.me/qr/…` contact chip (Surendra Kumar Rathi) | chip hidden |
| `WHATSAPP_URL_2` | `wa.me/qr/…` contact chip (Vasudev Toshniwal) | chip hidden |
| `MAPS_URL` | GET DIRECTIONS target (Maps search on the full address) | — |

`PHOTOS` (same block) lists the nine gallery photos with their face-crop
position, alt text, gallery caption and an inline base64 micro-thumbnail
(the marigold-swing portrait lives only in The Couple section).
`EVENTS` lists the six real events with their dates/times (add-to-calendar
buttons are generated from it).

Your live values are already wired in this file: both parents' lines, the
Apps Script `RSVP_ENDPOINT` (one sheet for RSVP + wishes), the WhatsApp
contact and the Maps links. Nothing to re-paste.

## One Google Sheet for RSVP + Wishes (5 minutes, free)

1. Create a Google Sheet (any name). **Extensions → Apps Script**, delete
   what is there and paste:

```js
/** RSVP + Wishes — one sheet. Columns:
 *  Timestamp | Type | Name | Side | Attending | Guests | Coming | Travel | Wish */
function doPost(e) {
  var d = JSON.parse(e.postData.contents);
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sh = ss.getSheetByName('Responses') || ss.insertSheet('Responses');
  if (sh.getLastRow() === 0)
    sh.appendRow(['Timestamp','Type','Name','Side','Attending','Guests','Coming','Travel','Wish']);
  sh.appendRow([
    new Date(), d.type || '', d.name || '',
    d.type === 'rsvp' ? (d.side || '') : '',
    d.type === 'rsvp' ? (d.attending ? 'Yes' : 'No') : '',
    d.type === 'rsvp' ? (d.guests || '') : '',
    d.type === 'rsvp' ? (d.when || '') : '',
    d.type === 'rsvp' ? (d.transport || '') : '',
    d.type === 'wish' ? (d.text || '') : ''
  ]);
  return ContentService.createTextOutput(JSON.stringify({ ok: true }))
    .setMimeType(ContentService.MimeType.JSON);
}
function doGet() {  // the wishes wall reads this
  var sh = SpreadsheetApp.getActiveSpreadsheet().getSheetByName('Responses');
  var out = { wishes: [] };
  if (sh) {
    var rows = sh.getDataRange().getValues();
    for (var i = 1; i < rows.length; i++) {
      if (rows[i][1] === 'wish')
        out.wishes.push({ n: rows[i][2], w: rows[i][7],
          t: rows[i][0] && rows[i][0].getTime ? rows[i][0].getTime() : Date.now() });
    }
  }
  return ContentService.createTextOutput(JSON.stringify(out))
    .setMimeType(ContentService.MimeType.JSON);
}
```

2. **Deploy → New deployment → ⚙ select "Web app"** →
   Execute as: **Me** · Who has access: **Anyone** → Deploy → authorise.
3. Copy the URL ending in `/exec`.
4. In `index.html` find `RSVP_ENDPOINT` and paste the URL between
   the quotes. Leave `WISHES_ENDPOINT: ''` — wishes then use the same
   sheet automatically.
5. Redeploy the site (`vercel --prod` or `git push`).

The site POSTs as JSON (Formspree-compatible); if the endpoint is an
Apps Script it transparently retries as `text/plain` (no CORS preflight)
— the row still lands. If the sheet is unreachable, guests fall back to
the WhatsApp flow, nothing is lost. Editing the script later?
**Deploy → Manage deployments → ✎ → Version: New version → Deploy**.

## Deploy to Vercel (exact steps)

**Option A — Vercel CLI (fastest, no GitHub):**

```bash
npm install -g vercel
cd bhavana-weds-mukund        # the folder containing index.html
vercel login                  # opens the browser; sign in with e-mail or GitHub
vercel                        # first run — answer:
                              #   Set up and deploy? → Y
                              #   Which directory?    → ./
                              #   Project name?       → bhavana-mukund (or Enter)
                              #   Override settings?  → N
                              # → prints a preview URL
vercel --prod                 # → https://bhavana-mukund.vercel.app is live
```

**Option B — GitHub + Vercel dashboard (auto-deploys on every push):**

```bash
cd bhavana-weds-mukund
git init && git add . && git commit -m "Wedding invite v3"
git branch -M main
git remote add origin https://github.com/<your-user>/bhavana-mukund.git
git push -u origin main       # repo created empty on github.com first
```

Then on **vercel.com** (sign up with GitHub) → **Add New → Project** →
Import the `bhavana-mukund` repo → Framework preset: **Other** →
**Deploy**. You get `https://bhavana-mukund.vercel.app`; rename it under
**Settings → Domains**, where you can also attach a custom domain later.

**Publishing changes to your existing bhavana-mukund.vercel.app:**

- **If you deployed with the CLI / drag-and-drop:** replace the folder
  contents with the new ones, then from the folder run `vercel --prod`
  (same login). That is all — the URL stays the same.
- **If you connected GitHub:** commit and push —
  `git add . && git commit -m "v3" && git push` — Vercel redeploys
  automatically.
- Via the dashboard: vercel.com → your project → **Deployments →
  ⋯ on the latest → Redeploy** only re-runs the old files; to upload new
  ones use the CLI method above or drag the folder into a GitHub repo.
- After redeploying, hard-refresh on the phone (Chrome → ⋮ → Refresh) or
  open in an incognito tab to bypass the cached copy.

## Notes

- Dates and times are fixed facts: 17–18 January 2027, Utsav, Vijay Bari,
  Vidyadhar Nagar, Jaipur (IST). Countdown target: 18 Jan, 7:00 pm IST
  (the wedding evening).
- "Add to calendar" generates a `.ics` (2-hour default duration); the
  Baraat & Varmala card generates both events in one file.
- Music begins once the doors stand open (browser autoplay rules are
  satisfied by the tap), volume 45%, looped; the nav button mutes/unmutes
  and the choice is remembered.
- The scratch card always loads covered in foil (Reset re-foils it).
- The gallery revolves by itself and pauses for your touch; the lightbox
  keeps it paused while open.
- Tested at 360/390/412/768/1440 px, dark scheme, reduced-motion tier and
  low-end tier; no horizontal scroll, no console errors.
