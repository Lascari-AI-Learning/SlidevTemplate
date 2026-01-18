---
allowed-tools: Read, Bash(mkdir:*), mcp__playwright__*
description: Capture screenshots for a specific slide template
arguments: --template=<template-name>
---

template_name = $ARGUMENTS

# Sync Template Screenshots

Capture screenshots for a single slide template showing all click states.

## Overview

This workflow captures progressive screenshots of a specific slide template, showing each v-click reveal state. Screenshots help agents understand:
- The visual layout and styling of the template
- How content progressively reveals through click states
- The storytelling flow of the slide

## Required Input

Extract the template name from the arguments:
- `--template=<name>` - The kebab-case template identifier (e.g., `title`, `intro-what-well-cover`)

If no template is provided, ask the user which template to sync.

## Workflow Steps

1. **Find Template** - Look up template in templates.json
2. **Calculate URL** - Determine the live slide URL from the order field
3. **Capture Screenshots** - Navigate to each click state and capture
4. **Save Files** - Store screenshots in the template's screenshots/ folder

---

## Step 1: Find Template

Read `templates.json` and locate the entry matching the requested template name.

**Action**: Read templates.json and find the slide entry where `template` matches the argument.

```
templates.json structure:
{
  "slides": [
    { "order": "00", "template": "title", "source": "slide.md", "clicks": 0 },
    { "order": "01", "template": "intro-what-well-cover", "source": "example.md", "clicks": 3 },
    ...
  ]
}
```

**Extract these fields from the matching entry**:
- `order` - The slide's position (e.g., "00", "01", "04")
- `clicks` - Number of click states to capture (0 means just the initial state)
- `template` - The template name (for folder path)

**Error handling**: If no matching template is found, report the error and list available templates.

---

## Step 2: Calculate URL

Calculate the slide URL from the order field.

**Base URL**: `http://localhost:3030/` (local dev server - must be running via `npm run dev`)

**Formula**:
```
slide_number = parseInt(order) + 1
```

**Examples**:
- order "00" → slide_number 1 → URL: `/1`
- order "04" → slide_number 5 → URL: `/5`
- order "99" → slide_number 100 → URL: `/100`

**Click state URLs**:
- Initial state (clicks=0): `/{slide_number}` (no query param needed)
- Click state n: `/{slide_number}?clicks={n}`

**Example for title template (order="00", clicks=0)**:
- Only URL: `http://localhost:3030/1`

**Example for intro-what-well-cover (order="01", clicks=3)**:
- click-0: `http://localhost:3030/2`
- click-1: `http://localhost:3030/2?clicks=1`
- click-2: `http://localhost:3030/2?clicks=2`
- click-3: `http://localhost:3030/2?clicks=3`

**Note**: Use localhost for capturing screenshots of new or updated templates. The live URL (`https://lascari-ai-learning.github.io/SlidevTemplate/`) is only up-to-date after deployment.

---

## Step 3: Capture Screenshots

Iterate through each click state and capture a screenshot using Playwright MCP tools.

**Loop**: For `n` from 0 to `clicks` (inclusive):

### 3a. Build URL for this click state

```
if n == 0:
    url = BASE_URL + slide_number
else:
    url = BASE_URL + slide_number + "?clicks=" + n
```

### 3b. Navigate to the URL

Use `mcp__playwright__browser_navigate`:
```
mcp__playwright__browser_navigate(url: "<full_url>")
```

### 3c. Wait for slide to render

Use `mcp__playwright__browser_wait_for` to ensure the slide is fully loaded:
```
mcp__playwright__browser_wait_for(time: 1)
```

### 3d. Take screenshot

Use `mcp__playwright__browser_take_screenshot` with the appropriate filename:
```
mcp__playwright__browser_take_screenshot(
    filename: "slide-templates/{template}/screenshots/click-{n}.png"
)
```

**Important**: Playwright MCP saves files to `.playwright-mcp/` prefix. After capture, move the file:
```bash
mv .playwright-mcp/slide-templates/{template}/screenshots/click-{n}.png slide-templates/{template}/screenshots/click-{n}.png
```

---

## Step 4: Ensure Screenshots Directory Exists

Before capturing screenshots, ensure the screenshots/ subdirectory exists.

**Action**: Create the directory if it doesn't exist:
```bash
mkdir -p slide-templates/{template}/screenshots/
```

**Directory structure**:
```
slide-templates/{template}/
├── description.md   # Usage documentation
├── example.md       # Example usage (if applicable)
├── slide.md         # Template with placeholders
└── screenshots/     # Click-state images (created by this workflow)
    ├── click-0.png  # Initial state
    ├── click-1.png  # After first click (if clicks > 0)
    └── ...          # Up to click-{clicks}.png
```

---

## Step 5: Report Completion

After all screenshots are captured, summarize the results:

**Success message format**:
```
## Sync Complete

Template: {template}
Screenshots captured: {clicks + 1} files
Location: slide-templates/{template}/screenshots/

Files created:
- click-0.png
- click-1.png (if applicable)
- ...
```

**If any errors occurred**, report them with the specific click state that failed.
