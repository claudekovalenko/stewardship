# Building & Blessing

What I am responsible for, and what I am only blessing.

One page. Two lists. Nothing else.

- **Mine to carry** — if it stalls, it stalls with me.
- **Blessing** — someone else carries it. Nice to get to, never ahead of the above.

## One field, with a key around it

Not a list. Every item is a bubble in a single packed composition, taken in at
one glance.

**The bubble carries a short, specific label** — up to three words, enough to name
the thing rather than gesture at it. The fuller phrase lives in a key ringing the
outside, joined to its bubble by a leader line. An item whose label already says
everything gets no key entry, which is most of them; the key exists for the ones
that genuinely need unpacking.

**It fits one screen.** Circles are sized to the tier, not to a sentence, and the
cluster is deliberately flat and small — the whole field, key, legend and add row
land inside a 1280×800 laptop without scrolling.

| Tier | | |
|---|---|---|
| **Deep** | solid, largest | Formation. These do not finish. |
| **Current** | tinted | Live responsibilities with edges. |
| **Blessing** | warm outline | I back it. Someone else owns it. |
| **Enjoyment** | amber outline | For gladness. No other reason. |
| **Future** | dotted | Not mine yet. Preparing. |

**Layout.** Labels are measured on a canvas, then circles pack along a spiral
from the centre — tier first, then your own order within the tier. Packing runs
outward, so order decides centrality: the first thing in Deep sits in the middle
and everything else gathers around it. Key entries are split left and right by which half of the field their
bubble sits in, distributed evenly down each side, and joined by a two-segment
leader drawn *behind* the bubbles. No layout library; about eighty lines.

The spiral's aspect ratio follows the viewport — wide on a desktop, tall and
narrow on a phone, where the ring is dropped for a two-column key beneath the
field. A wide composition scaled into a 390px screen renders type at a few
pixels; this keeps it at 13px+.

**The toggle** — All · Carrying · Blessing — fades the other side, key and
leaders included, to 14% rather than removing it. The composition never reflows.

**Tap a bubble or its key entry** to edit the short label, the key phrase and the
note separately, move it to any tier in one tap, or remove it.

## Live

<https://claudekovalenko.github.io/stewardship/> — deployed by GitHub Pages from
the `claude/responsibility-contributions-app-tvn4e0` branch. Because Pages serves
this from a subdirectory, every path in the app is relative; the manifest
`start_url`, `scope`, icons and the service worker all resolve inside
`/stewardship/`.

`.nojekyll` turns off Jekyll processing — this is a hand-written static site, and
Jekyll would otherwise skip any file whose name starts with `_`.

## Running it

Open `index.html`. No build step, no dependencies, no server; the app is one
self-contained file.

Served over HTTPS it is also an installable, offline-capable PWA — add it to a
home screen and it opens standalone. `manifest.webmanifest`, `sw.js` and the
icons do that; the service worker deliberately does not register from `file://`
or inside a frame.

## The list in this repo

`index.html` ships with a real list embedded in its `<script id="state">` block,
so the hosted copy loads with everything already in place rather than empty.
This is public, by the owner's explicit choice — anything added here is readable
by anyone. Keep genuinely private material out of it, or fork this to a private
repo and host it somewhere that deploys from one.

## Where the data lives

In your browser. Saved to `localStorage`, and — when published as a Claude
Artifact — written back into the published page so it follows you across
devices. No server, no account.

```jsonc
{
  "v": 2,
  "items": [
    { "id": "i1a2", "name": "Q3 platform migration", "list": "mine",   "target": null,   "from": null },
    { "id": "i3b4", "name": "Design system guild",   "list": "bless",  "target": null,   "from": null },
    { "id": "i5c6", "name": "On-call runbook",       "list": "switching", "target": "bless", "from": "mine" }
  ]
}
```

`list` is one of `mine`, `bless`, `switching`. An item in `switching` carries
`target` (where it is going) and `from` (where it came from, so cancelling puts
it back). Array order is priority order. Bad values are coerced on load and v1
data migrates automatically, so a hand-edited file cannot wedge the app.
