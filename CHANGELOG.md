# Changelog

All notable changes to this project are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Entries for 0.1.0 and 0.2.0 were reconstructed from the commit history after
the fact, so they summarise what shipped rather than what was recorded at the
time.

## [0.2.1] — 2026-07-26

### Fixed

- `.wf-screen` / `.wf-centered` — `100vh` ignored the 24px `body` padding, so
  every full-height wireframe overflowed by 48px and forced a scrollbar. Now
  `calc(100dvh - 48px)`, with a `vh` fallback for older engines.
- `.wf-avatar-group` — the white 2px border replaced each avatar's black
  outline instead of adding a separator between overlapping avatars, so groups
  rendered with no visible edge on a white page. Uses `outline` instead.
- `.wf-timeline-item` — the connector line sat at `-10px` while the dots centre
  at `-16px`, leaving them visibly misaligned.
- `.wf-btn-group` — a 1px right border meeting the next button's 2px left
  border drew a 3px seam between buttons.
- `.wf-select` — `appearance: none` stripped the native arrow without supplying
  a replacement, making the control indistinguishable from a text input.
- Package name reverted to the unscoped `chalk-css`. It had been renamed to
  `@okatarismet/chalk-css` with an `.npmrc` pointing at GitHub Packages, which
  contradicted every install instruction, badge and CDN URL in the README.
- The stylesheet header comment still read `v0.1.0`, two releases behind.

### Added

- `exports` map, so bundlers that ignore `main`/`style` resolve the stylesheet.
- `sideEffects: ["*.css"]`, so the documented `import 'chalk-css'` is not
  removed by tree-shaking.

## [0.2.0] — 2026-04-19

### Added

- `demo/index.html` — every component rendered on one page, no server needed.
- `COMPONENTS.md` — copy-paste HTML snippet for each component.
- Logo and hero screenshot.

## 0.1.0 — 2026-04-14

### Added

- Initial release: ~60 `wf-` classes in a single stylesheet covering layout
  primitives, app shell, typography, cards, forms, buttons, badges, tables,
  tabs, breadcrumbs, pagination, alerts, progress, steppers, kanban, timeline,
  dropdowns, avatars, media placeholders, modals, toasts and empty states.
- `README.md`, `AGENT-GUIDE.md` and `CONTRIBUTING.md`.

[0.2.1]: https://github.com/okatarismet/chalk/compare/v0.2.0...v0.2.1
[0.2.0]: https://github.com/okatarismet/chalk/releases/tag/v0.2.0
