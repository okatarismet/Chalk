# AGENT-GUIDE.md — Embedding Chalk into AI Agent Systems

This guide explains how to give any AI agent the ability to produce Chalk wireframes on demand. It covers system prompt design, usage rules, output conventions, and integration patterns for common agent frameworks.

---

## The core idea

An AI agent with Chalk in context can produce a fully renderable wireframe from a plain English description — in one pass, with no iteration, using a fraction of the tokens that custom CSS would require.

Instead of:
> "Design a search page with a centered search bar, some filter chips below it, and a results area."
> → AI writes 300 lines of custom CSS + HTML

With Chalk:
> Same prompt → AI picks 10 class names → done.

---

## Minimal system prompt snippet

Add this block to any agent's system prompt to unlock wireframe generation:

```
## Wireframe capability

You can produce browser-renderable wireframes using Chalk — a minimal, black-and-white HTML class library.

Rules:
- Always produce a complete, valid HTML file with <link rel="stylesheet" href="chalk.css">
- Use only the class names defined in the Chalk vocabulary (listed below)
- Do not write any custom CSS. Use inline style only for width and min-height on placeholder elements
- Output is black and white — do not add color of any kind
- File should open and render correctly in a browser with no build step

Vocabulary (prefix: wf-):
Layout:       screen, centered, row, col, layout, spacer, grid (cols-2/3/4)
Shell:        nav, topbar, sidebar (.wide/.narrow), main, panel, panel-header
Typography:   h1, h2, h3, h4, label, text, muted, placeholder, annotation, code, link
Box/Card:     box (.shaded/.dashed/.ghost), card (.compact), card-title, card-meta, card-footer, stat
Forms:        input (.large/.error), textarea, select, searchbar, field, field-error,
              checkbox (.checked), radio (.selected), toggle (.on)
Buttons:      btn (.primary/.secondary/.ghost/.danger/.sm/.lg/.full/.icon), btn-group
Badges:       badge (.dark/.outline/.pill/.dot), label, code, annotation
Table:        table (.compact)
Navigation:   tabs, tab-bar (.tab, .tab.active), tab-content, breadcrumb (.crumb, .sep),
              pagination (.page, .page.active, .page.disabled)
Feedback:     alert (.info/.warning/.error/.success), progress (.track, .fill),
              stepper (.step, .step-circle, .step-label, .step-line),
              toast (.dark), empty (.empty-icon, .empty-title, .empty-text)
Kanban:       kanban, kanban-col (.col-header, .col-body), kanban-card (.card-id)
Timeline:     timeline, timeline-item, timeline-dot (.filled), timeline-body,
              timeline-title, timeline-time, timeline-text
Modal:        modal-backdrop, modal (.modal-header, .modal-title, .modal-close,
              .modal-body, .modal-footer)
Media:        img, video, avatar (.sm/.lg/.xl/.square), avatar-group
Utility:      divider (.light/.dashed), note, redline, blueline
```

---

## Full system prompt template (drop-in)

```
You are a product design assistant. When asked to sketch, wireframe, or visualize a UI screen,
you produce a Chalk wireframe — a complete, browser-renderable HTML file.

## Output format
- Always output a full HTML file (<!DOCTYPE html> ... </html>)
- Link the stylesheet: <link rel="stylesheet" href="chalk.css">
- No JavaScript unless the user explicitly asks for interaction hints
- No inline styles except width and min-height on placeholder or sizing elements
- No custom CSS — only Chalk class names

## Design constraints
- Black and white only. Never add color.
- Monospace typography — the library handles this
- Boxes and labels, not polished UI — this is a sketch, not a final design
- Use wf-annotation or wf-note to call out unclear areas or design questions

## Naming convention
All class names are prefixed with wf-. Example: wf-card, wf-btn.primary, wf-modal.

## When to produce a wireframe
Trigger words: "sketch", "wireframe", "mock up", "draw", "visualize", "show me what this looks like",
"what would this screen look like", "prototype this"

## File naming
Name the output file after the screen: screen-dashboard.html, screen-login.html, screen-onboarding.html
```

---

## Integration patterns

### Claude (Anthropic API)

Pass the vocabulary block in the `system` field. Keep it in a cached prefix so it does not add cost on every turn.

```python
import anthropic

CHALK_SYSTEM = open("AGENT-GUIDE.md").read()  # or embed the snippet above

client = anthropic.Anthropic()
response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=4096,
    system=CHALK_SYSTEM,
    messages=[
        {"role": "user", "content": "Wireframe a user settings page with sections for profile, notifications, and billing."}
    ]
)
print(response.content[0].text)
```

### OpenAI / GPT-4

```python
from openai import OpenAI

client = OpenAI()
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": CHALK_SYSTEM_PROMPT},
        {"role": "user", "content": "Wireframe a kanban board with three columns."}
    ]
)
```

### Cursor / Windsurf / IDE agents

Add to your `.cursorrules` or project-level rules file:

```
When the user asks to sketch or wireframe a UI, produce a Chalk HTML file.
Use only wf- prefixed class names from chalk.css.
Never write custom CSS. Never add color.
Link the stylesheet: <link rel="stylesheet" href="path/to/chalk.css">
```

### Claude Code (slash command)

Create `.claude/commands/wireframe.md` in your project:

```markdown
# Wireframe

Produce a chalk.css wireframe for the described screen.

1. Identify what screen or component is being requested
2. Output a complete HTML file using only wf- class names from chalk.css
3. Name the file screen-{name}.html
4. Confirm the file path so the user can open it
```

---

## Prompting patterns that work well

### Describe the screen by function, not appearance

Good:
> "Wireframe a dashboard for a product manager — they need to see active agents, sprint progress, and a quick way to create a ticket."

Avoid:
> "Make it look modern and clean with cards."

### Ask for multiple screens at once

> "Wireframe the login screen, the onboarding flow (3 steps), and the main dashboard."

The model can generate all three in one pass.

### Use annotation to flag unknowns

Tell the agent to mark unclear areas:
> "Anywhere you're unsure about layout, add a wf-annotation so I know what to decide."

This produces wireframes with design questions baked in as readable notes.

### Iterate with diffs, not rewrites

> "On the dashboard wireframe: move the sidebar to the right side and add a timeline below the kanban board."

The agent can produce an updated file without regenerating from scratch.

---

## What the agent should NOT do

| Anti-pattern | Why |
|---|---|
| Write custom CSS | Defeats the purpose — adds tokens, breaks consistency |
| Add color via inline style | Wireframes are black and white by design |
| Use Tailwind or Bootstrap classes | They won't render without their own stylesheets |
| Produce React components | Unless explicitly asked — HTML is always the default |
| Omit the `<link>` tag | File won't render correctly |
| Use `wf-` classes that don't exist | Hallucinated classes are silently ignored by the browser |

---

## Validation checklist (for agent review step)

Before finalizing a wireframe output, an agent should verify:

- [ ] Output is a complete HTML file
- [ ] `<link rel="stylesheet" href="chalk.css">` is present in `<head>`
- [ ] No `<style>` blocks or custom CSS anywhere in the file
- [ ] No color values in inline styles (hex, rgb, named colors)
- [ ] All class names start with `wf-` or are modifier subclasses (`.active`, `.primary`, etc.)
- [ ] File opens correctly in a browser with `chalk.css` in the same directory

---

## Extending the library

Chalk is intentionally minimal. If a new primitive is needed:

1. Name it with the `wf-` prefix
2. Keep it black and white — no color variables
3. Add it to the vocabulary list in your system prompt
4. Document it in this guide

Do not modify the core `chalk.css` without bumping the version — agents cache the vocabulary at a point in time.

---

## Token budget reference

| Task | Approx tokens (output) |
|------|------------------------|
| Simple centered screen (search, login) | 100–200 |
| Dashboard with sidebar + table | 250–400 |
| Multi-section form with validation states | 200–350 |
| Full kanban board (3 columns, cards) | 300–500 |
| 3-screen onboarding flow | 400–700 |

Compare to generating equivalent layouts with custom CSS: typically 3–6× more tokens.
