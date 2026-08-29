# Building & Blessing

What I am responsible for, and what I am only blessing.

One page. Two lists. Nothing else.

- **Mine to carry** — if it stalls, it stalls with me.
- **Blessing** — someone else carries it. Nice to get to, never ahead of the above.

## The three things it does

**One priority stack.** Responsibilities are numbered `1..n`. Blessings continue
the *same* numbering below a hard line. There is no separate ranking, so a
blessing can never sit above a responsibility — the top blessing's "move up"
button is disabled, because above it is the line. The order on screen is the
order of your attention.

**Switching.** A thing in motion is neither one nor the other, so it gets its own
place. Press `⇄` on any item and it moves into a **Switching** band with a
direction — *handing off* or *taking on* — where it sits, counted on neither
side, until you confirm it landed. A handoff takes weeks; this makes those weeks
visible instead of pretending the change was instant.

**Editing.** Click a name and type. That is the whole editor.

| Control | Does |
|---|---|
| `▲` `▼` | Reorder — within that list only |
| `⇄` | Start a switch: hand off, or take on |
| `✕` | Remove |

Add with the field at the top. `Enter` adds to **Mine** — the default is that a
new thing is yours until you say otherwise.

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
