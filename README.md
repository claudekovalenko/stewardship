# Building & Blessing

What I am responsible for, and what I am only blessing.

One page. Two lists. Nothing else.

- **Mine to carry** — if it stalls, it stalls with me.
- **Blessing** — someone else carries it. Nice to get to, never ahead of the above.

## One field, seen at once

Not a list. Every item is a bubble in a single packed composition, so the whole
of it is one glance.

| | |
|---|---|
| **Deep** | solid — formation, these do not finish |
| **Current** | tinted — live responsibilities with edges |
| **Blessing** | outlined warm — I back it, someone else owns it |
| **Enjoyment** | outlined amber — for gladness, no other reason |
| **Future** | dotted — not mine yet, preparing |

Size carries meaning twice over: a tier floor (Deep bubbles are never small) plus
however much room the words need. Each circle is sized to its own wrapped label,
so text is legible at a fixed size rather than shrunk to fit a fixed circle.

**Layout.** Labels are measured on a canvas, wrapped into the line count that
yields the smallest enclosing circle, then packed largest-first along a spiral
from the centre in tier order — so what you carry settles in the middle and the
rest gathers around it. No layout library; the packing is about forty lines.

The spiral's aspect ratio follows the viewport: wide on a desktop, tall and
narrow on a phone. This matters more than it sounds — a wide composition scaled
into a 390px screen rendered labels at 7.6px. Narrowing the spiral and tightening
the tier floors on small screens brings that back to 15.6px without touching the
font size.

**The toggle** — All · Carrying · Blessing — fades the other side to 16% rather
than removing it. The composition never reflows, so the shape of the whole stays
put while you look at one half of it.

**Tap a bubble** to open it: rename, add a note, move it to any tier in one tap,
or remove it.

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
