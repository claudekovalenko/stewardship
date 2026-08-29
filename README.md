# Building & Blessing

A standing account of what you carry, and what you back.

One page, two registers:

| | Building | Blessing |
|---|---|---|
| The question | What am I responsible for? | What am I contributing to? |
| The claim | Mine to carry. If it stalls, it stalls with me. | Someone else's to carry. I lend weight, not ownership. |

The distinction is the whole point. Plenty of things take your time without being
yours to answer for, and it is easy to lose track of which is which. Every entry
has to declare a posture, so the register keeps the two honest.

## What it shows you

- **Load.** Each entry carries a weight, 1–5. The masthead bar splits the total
  between what you own and what you support, so you can see at a glance whether
  the balance is what you think it is.
- **My part.** The field that matters most — the specific accountability, not the
  activity. The editor prompts differently depending on the posture: *what breaks
  if you stop?* for Building, *name who actually owns it* for Blessing.
- **Drift.** Anything untouched for 60 days is flagged in red on the card and in
  the masthead count. Neglect shows up on its own; you don't have to go looking.
- **Ledger view.** The same entries as a sortable table, for a periodic review.
- **Share.** A plain-text summary of both registers, ready to paste into a
  one-on-one, a review doc, or a note to yourself.

## Running it

Open `index.html` in a browser. That's it — no build step, no dependencies, no
server. It is a single self-contained file.

```
git clone <this repo> && open index.html
```

## Where the data lives

Your entries never leave your browser.

- **Always:** saved to `localStorage` under `building-and-blessing/v1`.
- **When published as a Claude Artifact:** the page also saves each change back
  into its own published copy via the `artifact` capability, so the register
  follows you across devices instead of living in one browser profile.

Either way there is no server and no account. **Share & export → Data (JSON)**
copies everything out, and pastes it back in, so you are never locked in.

The app ships with six example entries to show the shape of the thing. They are
labelled as examples and one button clears them.

## Data model

```jsonc
{
  "v": 1,
  "demo": false,
  "entries": [{
    "id": "e1a2b3",
    "posture": "building",        // "building" | "blessing"
    "name": "Q3 platform migration",
    "what": "One line, for someone who has never heard of it.",
    "part": "The specific accountability.",
    "weight": 5,                   // 1–5, what it costs you
    "status": "Active",            // Starting | Active | Steady | Winding down | Paused
    "people": "Who else is in it",
    "next": "The one thing that would move this",
    "link": "https://…",           // http(s) only; anything else is dropped
    "touched": "2026-08-26"        // ISO date
  }]
}
```

Unknown fields are dropped and bad values are coerced on import, so a
hand-edited file can't put the app into a broken state.
