# Contributing to Chalk

Thanks for your interest. Chalk is intentionally small — contributions should keep it that way.

---

## Philosophy

Every addition must pass this test:

> "Would an AI produce better wireframes with this, using fewer tokens?"

If yes, it belongs. If it adds visual complexity, requires JavaScript, or introduces color, it does not.

---

## Adding a new component

1. The class name must start with `wf-`
2. Black and white only — no color values anywhere
3. No JavaScript dependencies
4. Add the component to `chalk.css` under the correct section header
5. Add it to the vocabulary table in `README.md`
6. Add it to the vocabulary list in `AGENT-GUIDE.md`
7. Add a usage example in the README component reference
8. Add a demo in `demo/index.html`

---

## What we won't add

- Color variants (even "neutral" grays beyond what's already there)
- Animations or transitions
- JavaScript-dependent components
- Components that duplicate existing primitives
- Design-specific patterns (charts, maps, rich text editors)

---

## Versioning

chalk.css follows semver. Because AI agents cache the vocabulary, breaking changes (renamed or removed classes) require a major version bump.

- **Patch** (0.1.x): bug fixes, rendering corrections
- **Minor** (0.x.0): new components added, nothing removed
- **Major** (x.0.0): classes renamed or removed

---

## Reporting issues

If a class doesn't render as expected, open an issue with:
- The HTML snippet that produced the problem
- Which browser and version
- A description of what you expected vs. what you saw
