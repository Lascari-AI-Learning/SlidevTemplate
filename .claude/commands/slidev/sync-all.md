---
allowed-tools: Read, Bash(mkdir:*), mcp__playwright__*
description: Capture screenshots for all slide templates
---

# Sync All Template Screenshots

Capture screenshots for ALL slide templates showing each click state.

## Overview

This workflow iterates through every template in `templates.json` and captures progressive screenshots for each. This ensures the entire template library has up-to-date visual documentation.

**What this captures**:
- Every template listed in templates.json
- All click states for each template (from initial state through final reveal)
- Screenshots saved to each template's `screenshots/` folder

**Why this matters**:
- Agents can visually understand template layouts and styling
- Progressive screenshots show the storytelling flow of each slide
- Consistent documentation across the entire template library

## Workflow Steps

1. **Load Templates** - Read templates.json to get all slide entries
2. **Iterate and Capture** - For each template, navigate to each click state and screenshot
3. **Report Summary** - Show total templates synced and screenshot counts

---

## Step 1: Load Templates

Read `templates.json` to get the list of all slides.

**Action**: Read templates.json and extract the `slides` array.

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

**For each slide entry, you will need**:
- `order` - The slide's position (used to calculate URL)
- `template` - The template name (used for folder path)
- `clicks` - Number of click states to capture

**Current templates (as of last update)**: 9 templates

---

## Step 2: Iterate and Capture

For EACH slide entry in templates.json, capture all click states.

### 2a. Create screenshots directory

Before capturing, ensure the screenshots folder exists:

```bash
mkdir -p slide-templates/{template}/screenshots/
```

### 2b. Calculate URL

**Base URL**: `http://localhost:3030/` (local dev server - must be running via `npm run dev`)

**Formula**:
```
slide_number = parseInt(order) + 1
```

**Click state URLs**:
- Initial state (n=0): `/{slide_number}` (no query param needed)
- Click state n > 0: `/{slide_number}?clicks={n}`

### 2c. Capture loop

For each template, loop from `n = 0` to `clicks` (inclusive):

1. **Build URL**:
   ```
   if n == 0:
       url = "http://localhost:3030/" + slide_number
   else:
       url = "http://localhost:3030/" + slide_number + "?clicks=" + n
   ```

2. **Navigate**:
   ```
   mcp__playwright__browser_navigate(url: "<full_url>")
   ```

3. **Wait for render**:
   ```
   mcp__playwright__browser_wait_for(time: 1)
   ```

4. **Capture screenshot**:
   ```
   mcp__playwright__browser_take_screenshot(
       filename: "slide-templates/{template}/screenshots/click-{n}.png"
   )
   ```

5. **Move file** (Playwright saves to `.playwright-mcp/` prefix):
   ```bash
   mv .playwright-mcp/slide-templates/{template}/screenshots/click-{n}.png slide-templates/{template}/screenshots/click-{n}.png
   ```

### 2d. Repeat for all templates

Continue through the entire `slides` array until all templates have been captured.

---

## Step 3: Report Summary

After all screenshots are captured, provide a completion summary.

**Success message format**:

```
## Sync All Complete ✅

Templates synced: {count} templates
Total screenshots: {total} files

### Per-Template Breakdown:
| Template | Clicks | Screenshots |
|----------|--------|-------------|
| title | 0 | 1 |
| intro-what-well-cover | 3 | 4 |
| about-me | 0 | 1 |
| ... | ... | ... |

All screenshots saved to slide-templates/{template}/screenshots/
```

**If any errors occurred**, list the specific templates and click states that failed.

---

## Expected Results

Based on current templates.json, sync-all should capture:

| Template | Clicks | Screenshots |
|----------|--------|-------------|
| title | 0 | 1 |
| intro-what-well-cover | 3 | 4 |
| about-me | 0 | 1 |
| icon-list-content | 2 | 3 |
| continuum-diagram | 4 | 5 |
| extremes-to-middle | 2 | 3 |
| continuum-middle-ground | 3 | 4 |
| three-to-one-takeaway | 4 | 5 |
| conclusion-lets-connect | 0 | 1 |

**Total**: 9 templates, 27 screenshots
