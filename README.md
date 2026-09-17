# Concept Bank

A static hub that auto-lists whatever concepts exist under `/concepts/`. There is nothing to register anywhere — the hub page asks GitHub's API what folders exist under `concepts/` and builds the list from that, every time it loads.

## Structure

```
concept-bank/
├── index.html                     ← the hub / picker page (auto-discovers concepts)
└── concepts/
    ├── example-one/
    │   ├── index.html             ← the concept itself, fully self-contained
    │   └── meta.json              ← optional: name / description / tags
    └── example-two/
        ├── index.html
        └── meta.json
```

## Adding a new concept

1. Create a folder under `concepts/`, e.g. `concepts/my-real-concept/`.
2. Put your concept's HTML inside it, named `index.html`.
3. Push it to GitHub. That's it — refresh the hub page and it'll show up.

No file needs editing. The folder name itself becomes the title (e.g. `retro-timer` → "Retro Timer") unless you add a `meta.json`.

### Optional: `meta.json`

Drop this next to a concept's `index.html` if you want a nicer name, a one-line description, or tags:

```json
{
  "name": "Retro Timer",
  "desc": "A CRT-styled countdown, just for fun.",
  "tags": ["timer", "retro"]
}
```

All fields are optional — leave out anything you don't need, or skip the file entirely.

## Important: this only auto-detects when hosted on GitHub Pages

The hub calls `api.github.com` to list the contents of `/concepts/`, which only works when the page is actually served from `<owner>.github.io/<repo>/`. If you open `index.html` straight from your file system (`file://...`), there's no API to ask, so the hub will show a message instead of a list — in that case just open the concept's `index.html` directly from its folder.

It also assumes this hub's `index.html` sits at the **root of its own repository** (so the URL is `https://<owner>.github.io/<repo>/`, and `concepts/` is right there next to it). If you nest it deeper inside a bigger repo, the auto-detected repo name won't line up — let me know and I can adjust the detection logic.

## A couple of small caveats

- GitHub's API allows 60 unauthenticated requests per hour per visitor — plenty for personal use, but if it's ever hit, the hub shows a "rate limited, try again shortly" message rather than an empty page.
- Renaming a folder is exactly like adding a new one: rename it, push, refresh.
- If a concept needs to be its own installable offline PWA (like TimeBack), give it its own `manifest.json` and `sw.js` inside its folder and register the service worker from within that concept's `index.html` — it stays scoped to that folder and won't affect the hub or other concepts.
