# Concept Bank

A static hub that lists a growing collection of independent HTML concepts. Each concept is its own self-contained page — its own HTML/CSS/JS, no shared dependencies — so you can add, remove, or rework any one of them without touching the others.

## Structure

```
concept-bank/
├── index.html                     ← the hub / picker page (searchable list)
└── concepts/
    ├── example-one/
    │   └── index.html             ← a concept, fully self-contained
    └── example-two/
        └── index.html
```

## Adding a new concept

1. Create a new folder under `concepts/`, e.g. `concepts/my-new-idea/`.
2. Put a self-contained `index.html` inside it (any CSS/JS should live inline in that file, or in files inside that same folder — don't rely on anything from the hub or other concepts).
3. Open `index.html` (the hub page) and add one line to the `CONCEPTS` array near the top of the `<script>` tag:

   ```js
   const CONCEPTS = [
     { name: 'My new idea', path: 'my-new-idea', desc: 'One line about it.', tags: ['sketch'] },
   ];
   ```

   - `path` must exactly match the folder name under `concepts/`.
   - `desc` and `tags` are optional — leave them out if you don't need them.

That's it — no build step, no server required. Just open `index.html` in a browser (or host the whole folder anywhere that serves static files, like GitHub Pages).

## Removing / renaming a concept

Delete (or rename) its folder under `concepts/`, and remove (or update) its matching entry in the `CONCEPTS` array.

## Notes

- Links use relative paths (`concepts/<folder>/index.html`), so the whole thing works identically whether it's opened straight from disk, hosted on GitHub Pages, or served from any static host.
- If a concept needs to be an installable offline PWA on its own (like TimeBack), give it its own `manifest.json` and `sw.js` inside its folder and register the service worker from within that concept's `index.html` — it'll stay scoped to that folder and won't affect the hub or other concepts.
