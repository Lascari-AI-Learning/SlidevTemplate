---
name: slidev
description: Slidev template system conventions and workflow commands. Use when creating slides, managing templates, capturing screenshots, or understanding the slide template structure.
---

# Slidev Template System

## Overview

This project uses a template-based system for creating Slidev presentations. Each template provides:

- **Visual examples** - Screenshots showing progressive click states
- **Documentation** - Usage instructions and best practices
- **Reusable structure** - Markdown templates with placeholder variables

### Purpose

The template system enables agents to understand slide storytelling through visual context. Screenshots show not just the final layout, but the progression of elements at each click state - critical for understanding how information reveals during a presentation.

### Key Components

| Component | Location | Purpose |
|-----------|----------|---------|
| Template folders | `slide-templates/{name}/` | Individual template files and screenshots |
| Template registry | `templates.json` | Index of all templates with metadata |
| Screenshot capture | Playwright MCP | Automated visual capture at each click state |
| Workflow commands | `.claude/commands/slidev/` | Agent-driven template management |

## Commands

Three workflow commands are available for managing templates:

### `/slidev:sync-template`

Capture screenshots for a **single** template.

```
/slidev:sync-template --template=title
```

**Use when**: A specific template has been updated and needs fresh screenshots.

**Process**:
1. Reads `templates.json` to find the template entry
2. Calculates slide URL from `order` field
3. Navigates to each click state using Playwright MCP
4. Captures screenshots to `slide-templates/{template}/screenshots/`

**Requirements**: Local dev server must be running (`npm run dev`)

---

### `/slidev:sync-all`

Capture screenshots for **all** templates in templates.json.

```
/slidev:sync-all
```

**Use when**:
- Initial setup of template screenshots
- After bulk updates to styling
- Periodic refresh of visual documentation

**Process**:
1. Reads all entries from `templates.json`
2. Iterates through each template
3. Captures screenshots for every click state
4. Reports summary with totals

**Requirements**: Local dev server must be running (`npm run dev`)

---

### `/slidev:add-template`

**Interactive** workflow for creating a new template.

```
/slidev:add-template
```

**Use when**: Adding a new slide template to the library.

**Process**:
1. Prompts for template name (kebab-case identifier)
2. Asks about purpose and content type
3. Gathers layout structure details
4. Determines animation/click pattern
5. Creates folder structure with all required files
6. Updates `templates.json` with new entry
7. Reminds to deploy, then captures screenshots

**Creates**:
- `slide-templates/{name}/description.md` - Usage documentation
- `slide-templates/{name}/slide.md` - Template with placeholders
- `slide-templates/{name}/example.md` - Sample content with v-clicks
- `slide-templates/{name}/screenshots/` - Click-state images

## Conventions

### Naming

- **Template identifiers**: Use `kebab-case` (e.g., `intro-what-well-cover`, `three-to-one-takeaway`)
- **Screenshot files**: `click-{n}.png` where n starts at 0
- **Slide files**: Numbered prefix in `slides/` directory (e.g., `01-about-me.md`, `02-introduction.md`)

### Folder Structure

Each template lives in `slide-templates/{template-name}/`:

```
slide-templates/{template-name}/
├── description.md   # Usage documentation
├── example.md       # Example with sample content
├── slide.md         # Template with {{placeholders}}
└── screenshots/     # Click-state images
    ├── click-0.png  # Initial state
    ├── click-1.png  # After first click
    └── click-N.png  # Up to clicks value
```

### URL Patterns

**Local development**: `http://localhost:3030/{slide_number}?clicks={n}`

**Live deployment**: `https://lascari-ai-learning.github.io/SlidevTemplate/{slide_number}?clicks={n}`

**URL calculation**:
```
slide_number = parseInt(order) + 1
```

| Order | Slide Number | Base URL |
|-------|--------------|----------|
| "00"  | 1            | /1       |
| "04"  | 5            | /5       |
| "99"  | 100          | /100     |

### Click States

- `clicks=0` (or no param): Initial slide state
- `clicks=1`: After first v-click reveal
- `clicks=N`: After N reveals

The `clicks` field in `templates.json` indicates the total number of v-click transitions. A template with `clicks: 3` will have 4 screenshots (click-0 through click-3).

## References

- **[Template Structure](references/templates.md)** - Folder structure and templates.json schema
- **[Playwright Workflow](references/playwright-workflow.md)** - Screenshot capture patterns
