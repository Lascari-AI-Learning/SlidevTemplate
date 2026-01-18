---
allowed-tools: AskUserQuestion, Write, Edit, Read, Bash(mkdir:*), mcp__playwright__*
description: Interactive workflow for adding new slide templates
---

# Add New Slide Template

Interactive workflow for creating a new Slidev template with proper structure, documentation, and screenshot capture.

## Step 1: Template Name

Ask the user for a template identifier using kebab-case naming convention.

**Instructions**:
1. Use AskUserQuestion to prompt for the template name
2. Name should be kebab-case (e.g., `two-column-compare`, `timeline-horizontal`)
3. Validate the name doesn't already exist in `slide-templates/`

**Example prompt**:
```
What is the template name? (use kebab-case, e.g., "two-column-compare")
```

Store the result as `template_name` for use in subsequent steps.

## Step 2: Template Purpose

Ask the user to describe the template's purpose.

**Instructions**:
1. Use AskUserQuestion to prompt for the template purpose
2. Should describe what kind of content/story the template presents
3. Examples: "Show progression from one concept to another", "Compare two options side by side"

**Example prompt**:
```
What is the purpose of this template? Describe what kind of content it presents.
(e.g., "Show a timeline of events", "Compare pros and cons of two options")
```

Store the result as `template_purpose` for use in documentation.

## Step 3: Layout Structure

Ask the user about the visual layout and structure.

**Instructions**:
1. Use AskUserQuestion to prompt for layout details
2. Ask about: number of columns, sections, key visual elements
3. Gather information needed to build the slide.md template

**Example prompt**:
```
Describe the layout structure:
- How many columns or sections?
- What visual elements? (icons, images, diagrams, cards)
- Any special positioning? (centered, grid, flex)
```

Store the result as `layout_structure` for building the template.

## Step 4: Animation Pattern

Ask the user about the v-click reveal strategy.

**Instructions**:
1. Use AskUserQuestion to prompt for animation pattern
2. Ask about how elements should progressively reveal
3. Common patterns: all-at-once, sequential items, section-by-section

**Example prompt**:
```
How should elements animate/reveal?
- All visible at once (clicks: 0)
- Sequential reveal of each item
- Section-by-section reveal
- Custom pattern (describe)
```

Store the result as `animation_pattern` for building the example.md with v-click annotations.

## Step 5: Create Folder Structure

Create the template folder and subdirectories.

**Instructions**:
1. Create `slide-templates/{template_name}/` directory
2. Create `slide-templates/{template_name}/screenshots/` subdirectory

**Commands**:
```bash
mkdir -p slide-templates/{template_name}/screenshots
```

**Expected structure**:
```
slide-templates/{template_name}/
├── screenshots/     # Will contain click-state images later
├── description.md   # Created in Step 6
├── slide.md         # Created in Step 7
└── example.md       # Created in Step 8
```

## Step 6: Generate description.md

Create the documentation file explaining the template.

**Instructions**:
1. Use the Write tool to create `slide-templates/{template_name}/description.md`
2. Generate content based on user inputs from Steps 1-4

**Template structure**:
```markdown
# {Template Name (Title Case)}

## Purpose
{template_purpose from Step 2}

## When to Use
- {Generate 3-4 bullet points based on purpose}

## Template Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `{{variable_name}}` | Description | Example value |
{Generate variables based on layout_structure from Step 3}

## Animation Behavior
{animation_pattern from Step 4}
- clicks: {number based on animation}

## Visual Features
{Describe key visual elements from layout_structure}
```

Use the user's responses to populate each section appropriately.

## Step 7: Generate slide.md

Create the template file with placeholder variables.

**Instructions**:
1. Use the Write tool to create `slide-templates/{template_name}/slide.md`
2. Start with frontmatter: `theme: ../` and `layout: default`
3. Build HTML structure based on `layout_structure` from Step 3
4. Use `{{variable}}` for simple placeholders
5. Use `{{{variable}}}` for HTML content (triple braces)
6. Use `{{#each items}}...{{/each}}` for arrays
7. Use `{{#if condition}}...{{/if}}` for conditionals

**Template structure**:
```markdown
---
theme: ../
layout: default
---

<div class="...">
  {{title}}

  {{#each items}}
  <div v-click>
    {{this.content}}
  </div>
  {{/each}}
</div>

<!--
{{speaker_notes}}
-->
```

**Styling notes**:
- Use Tailwind CSS classes for styling
- Use `v-click` directive for animations
- Include `speaker_notes` variable at the bottom in HTML comments

## Step 8: Generate example.md

Create an example file with sample content and v-click animations.

**Instructions**:
1. Use the Write tool to create `slide-templates/{template_name}/example.md`
2. Copy the structure from slide.md but replace placeholders with concrete values
3. Add `<v-click>` or `v-click` directive based on `animation_pattern` from Step 4
4. Use realistic sample content that demonstrates the template's purpose

**Template structure**:
```markdown
---
theme: ../
layout: default
---

<div class="...">
  Example Title Here

  <v-click>
  <div>
    First item content
  </div>
  </v-click>

  <v-click>
  <div>
    Second item content
  </div>
  </v-click>
</div>

<!--
These are sample speaker notes explaining the slide.
-->
```

**Animation notes**:
- Use `<v-click>` wrapper for block elements
- Use `v-click` attribute for inline elements
- Use `<v-click at="N">` to control timing order
- Count total v-click elements to determine `clicks` value for templates.json

## Step 9: Analyze Click Count

Count v-click elements to determine the `clicks` field for templates.json.

**Instructions**:
1. Read the generated `example.md` file
2. Count all `<v-click>` and `v-click` occurrences
3. Find the highest `at="N"` value if explicit timing is used
4. The `clicks` value = max(count of v-clicks, highest at value)

**Counting rules**:
- Each `<v-click>` wrapper = 1 click
- Each `v-click` attribute = 1 click
- `<v-click at="5">` means at least 5 clicks needed
- If no v-clicks, `clicks` = 0

**Examples**:
- 3 `<v-click>` wrappers → `clicks: 3`
- 2 `<v-click>` + 1 `<v-click at="4">` → `clicks: 4`
- No v-clicks → `clicks: 0`

Store the result as `click_count` for templates.json update.

## Step 10: Update templates.json

Add the new template entry to templates.json.

**Instructions**:
1. Read `templates.json` to get current entries
2. Determine the next available `order` value (find highest order < 99, add 1)
3. Add new entry to the `slides` array before the conclusion slide (order: 99)

**Entry structure**:
```json
{
  "order": "08",
  "template": "{template_name}",
  "source": "example.md",
  "clicks": {click_count}
}
```

**Field values**:
- `order`: 2-digit string, next available number (e.g., "08", "09")
- `template`: The `template_name` from Step 1 (kebab-case)
- `source`: Usually "example.md" (the file with concrete values)
- `clicks`: The `click_count` from Step 9

**Important**:
- Keep entries sorted by order
- The conclusion slide (order: "99") should always be last
- Use the Edit tool to add the new entry

## Step 11: Deploy

Remind the user to deploy the presentation before capturing screenshots.

**Important**: Screenshots are captured from the live URL:
`https://lascari-ai-learning.github.io/SlidevTemplate/`

**Instructions**:
1. Inform the user that deployment is required before screenshots can be captured
2. The new template must be live at the URL for Playwright MCP to capture it
3. Provide the deployment commands:

**Deployment steps**:
```bash
# Build the slides (regenerate index.md from slides/)
npm run build:slides

# Build for production
npm run build

# Commit and push to trigger GitHub Pages deployment
git add .
git commit -m "Add {template_name} template"
git push
```

**Wait for deployment**: GitHub Pages deployment typically takes 1-2 minutes. Verify the new slide is accessible at the live URL before proceeding to Step 12.

## Step 12: Capture Screenshots

After deployment, capture screenshots using the sync-template workflow.

**Instructions**:
1. Ensure the local dev server is running (`npm run dev`) or use the live URL
2. Follow the sync-template workflow to capture all click states

**Option A - Use the sync-template command**:
```
/slidev:sync-template --template={template_name}
```

**Option B - Manual capture using Playwright MCP**:

For each click state (n = 0 to click_count):

1. **Navigate to the slide**:
   ```
   mcp__playwright__browser_navigate(url: "http://localhost:3030/{slide_number}?clicks={n}")
   ```
   (Note: For n=0, omit the `?clicks=0` query param)

2. **Wait for render**:
   ```
   mcp__playwright__browser_wait_for(time: 1)
   ```

3. **Capture screenshot**:
   ```
   mcp__playwright__browser_take_screenshot(
       filename: "slide-templates/{template_name}/screenshots/click-{n}.png"
   )
   ```

4. **Move from .playwright-mcp/ to final location**:
   ```bash
   mv .playwright-mcp/slide-templates/{template_name}/screenshots/click-{n}.png \
      slide-templates/{template_name}/screenshots/click-{n}.png
   ```

**Completion**: Once all screenshots are captured, the template is fully set up and ready for use.
