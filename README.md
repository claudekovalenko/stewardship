# Building & Blessing

What I am responsible for, and what I am only blessing.

One page. Two lists. Nothing else.

- **Mine to carry** — if it stalls, it stalls with me.
- **Blessing** — someone else carries it. Nice to get to, never ahead of the above.

## Five tiers, one stack

| Tier | | |
|---|---|---|
| **Deep** | numbered | Formation. These do not finish, and nobody else can do them for me. |
| **Current** | numbered | Live responsibilities with edges. Real, but not the deep work. |
| — | | *not mine to carry* |
| **Blessing** | listed | I back it. Someone else owns it. |
| **Enjoyment** | listed | For gladness. No other reason needed. |
| **Future** | listed | Not mine yet. The work now is preparing. |

**Deep** and **Current** share one continuous numbering — `1..n` straight
through both — because they are the same stack of attention. The three tiers
below the line are listed, not ranked; they do not compete with what you carry.

**`▲` and `▼` do one job in two ways.** Inside a tier they reorder. At a tier's
edge they carry the item across into the neighbouring tier. So promoting a
future hope into a live responsibility, or handing a current one down to a
blessing, is the same gesture as reordering — the page is a single stack, and
only the very first and very last item have a disabled control.

**Notes** are optional, one per item, opened with `✎` and shown in italic under
the name. They open on an explicit press, never on hover: revealing a field on
hover changes the row's height, which shifts every row below it out from under
the pointer and makes the next click land on the wrong item.

Click any name or note to edit it in place. Both grow to fit what you type.

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
