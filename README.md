# Bhavana & Mukund — The Royal Gateway (v2.1)

A single-file, scroll-driven Jaipur wedding invitation.
Open `index.html` in any modern browser, or deploy the whole folder to
Vercel (steps below) — any static host works, no build step.

## What is inside

```
index.html            the whole site (CSS + JS inline, ~222 KB)
images/
  photo-01..10.webp   the couple's 10 photos (lazy-loaded, <=290 KB each)
  og-cover.jpg        WhatsApp / social preview card (1200x630)
audio/
  mangal-rang.mp3     "Mangal Rang Hai Prem Ke Rango Ka Sangam"
                      (552 KB — plays when the gate opens; mute button in the nav)
```

## What changed in v2.1

- Full venue address on the Venue card + GET DIRECTIONS now searches
  Google Maps for `Utsav, 197, Sector 2 Rd, Vijay Bari, Vidyadhar Nagar,
  Jaipur, Rajasthan 302039`.
- "Royal" wording removed from section headings (The Couple, The
  Festivities, Our Gallery) — it now only appears in the browser tab /
  share card title.
- The duplicate "Add us on WhatsApp" block after the RSVP form is gone.
  The one in Guest Guide → Contact stays.
- The couple frame now shows the holding-hands photo (`photo-04`),
  and the blur-up thumb no longer covers the sharp photo.
- RSVP replies and guest wishes can both land in **one Google Sheet**
  (setup below). Until you paste the URL, the site falls back to the
  WhatsApp reply flow and a this-device wish wall.
- Memories QR stays hidden until you fill `PHOTO_GALLERY_URL` (later).

## Edit me — the CONFIG block (top of the script in index.html)

| Key | Meaning | While empty |
|---|---|---|
| `GROOM.parents` / `BRIDE.parents` | "Son/Daughter of … and …" lines | the line hides itself |
| `COUPLE.groomPhoto` / `bridePhoto` | photo ids (`'photo-05'`) for the two-frame layout | couple photo in one centred frame |
| `COUPLE.couplePhoto` | photo id for the centred couple frame (photo-04, holding hands) | — |
| `DOOR_IMG` | front view of a symmetric double door → put the file at `images/door.jpg` | built-in SVG doors |
| `REVEAL_IMG` | bright scene behind the opening doors → `images/reveal.jpg` | golden glow |
| `MUSIC_SRC` | currently `audio/mangal-rang.mp3` | music toggle hidden |
| `PHOTO_GALLERY_URL` | Kamero / PicsDrop gallery link (Memories QR) | gold frame + "link coming soon" |
| `HASHTAG` | shown in the closing sign-off | hidden |
| `RSVP_ENDPOINT` | Google Apps Script web-app URL or Formspree ID | WhatsApp message flow |
| `WISHES_ENDPOINT` | separate URL; empty = **reuse `RSVP_ENDPOINT`** (one sheet, `type` column splits rows) | this-device wish wall |
| `MAPS_URL` | GET DIRECTIONS target (Maps search on the full address) | — |
| `FAMILY_MEMBERS` | `[{name, relation, side:'groom'\|'bride', photo}]` | Our-Family section hidden |
| `GUIDE.pickups` / `GUIDE.stay` | extra guest-guide lines | hidden |

`PHOTOS` (same block) lists the ten photos with their face-crop position,
alt text, gallery caption and an inline base64 micro-thumbnail.

## One Google Sheet for RSVP + Wishes (5 minutes, free)

1. Create a Google Sheet (any name). **Extensions → Apps Script**, delete
   what is there and paste:

```js
/** RSVP + Wishes — one sheet. Columns:
 *  Timestamp | Type | Name | Attending | Guests | Events | Notes | Wish */
function doPost(e) {
  var d = JSON.parse(e.postData.contents);
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sh = ss.getSheetByName('Responses') || ss.insertSheet('Responses');
  if (sh.getLastRow() === 0)
    sh.appendRow(['Timestamp','Type','Name','Attending','Guests','Events','Notes','Wish']);
  sh.appendRow([
    new Date(), d.type || '', d.name || '',
    d.type === 'rsvp' ? (d.attending ? 'Yes' : 'No') : '',
    d.type === 'rsvp' ? (d.guests || '') : '',
    d.type === 'rsvp' ? ((d.events || []).join('; ')) : '',
    d.type === 'rsvp' ? (d.notes || '') : '',
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
4. In `index.html` find `RSVP_ENDPOINT: ''` and paste the URL between
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
git init && git add . && git commit -m "Wedding invite v2.1"
git branch -M main
git remote add origin https://github.com/<your-user>/bhavana-mukund.git
git push -u origin main       # repo created empty on github.com first
```

Then on **vercel.com** (sign up with GitHub) → **Add New → Project** →
Import the `bhavana-mukund` repo → Framework preset: **Other** →
**Deploy**. You get `https://bhavana-mukund.vercel.app`; rename it under
**Settings → Domains**, where you can also attach a custom domain later.

**Publishing later changes:** edit the files → `vercel --prod`
(Option A) or `git add . && git commit -m "…" && git push` (Option B) —
Vercel redeploys automatically.

## Notes

- Dates and times are fixed facts: 17–18 January 2027, Utsav, Vijay Bari,
  Vidyadhar Nagar, Jaipur (IST).
- "Add to calendar" generates a `.ics` (2-hour default duration).
- Music starts on the gate-open tap (browser autoplay rules), volume 45%,
  looped; the nav button mutes/unmutes and the choice is remembered.
- Tested at 360/390/412/768/1440 px, dark scheme, reduced-motion tier and
  low-end tier; no horizontal scroll, no console errors.
