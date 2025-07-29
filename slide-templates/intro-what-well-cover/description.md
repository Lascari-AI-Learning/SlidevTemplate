# Intro / What We'll Cover Template

## Purpose
This template creates an overview slide showing multiple topics or sections that will be covered in the presentation. Each section is displayed in a card with an icon, title, subtitle, and bullet points.

## When to Use
- Early in your presentation to set expectations
- To provide a roadmap of topics you'll cover
- When you need to organize content into 2-4 main sections
- For agenda or overview slides

## Template Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `{{main_title}}` | The slide's main heading | "What We'll Cover Today" |
| `{{columns}}` | Number of columns (2-4) | 3 |
| `{{sections}}` | Array of section objects | See section structure below |
| `{{speaker_notes}}` | Speaker notes for the slide | "This slide sets the stage..." |

### Section Structure
Each section in the `{{sections}}` array should have:

| Property | Description | Example |
|----------|-------------|---------|
| `title` | Section title | "A Holistic View" |
| `color` | Color theme (tailwind colors) | "purple", "sky", "emerald" |
| `icon_path` | SVG path for the icon | "M9 12l2 2 4-4m5.618..." |
| `subtitle` | Section subtitle | "Understanding Claude Code" |
| `points` | Array of bullet points | ["What It Actually Is", "Where It Fits"] |
| `center_title` | Optional: center the title | true/false |
| `extra_margin` | Optional: add extra top margin | true/false |

## Usage Example

```bash
npm run generate:slide -- --template=intro-what-well-cover --name=01-what-well-cover \
  --main_title="What We'll Cover Today" \
  --columns=3 \
  --sections='[
    {
      "title": "A Holistic View",
      "color": "purple",
      "icon_path": "M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944...",
      "subtitle": "Understanding Claude Code",
      "points": ["What It Actually Is", "Where It Fits in the Ecosystem"]
    },
    {
      "title": "The Differentiator",
      "color": "sky",
      "icon_path": "M13 10V3L4 14h7v7l9-11h-7z",
      "subtitle": "What Makes It Different",
      "points": ["Agentic with Visibility", "Engineer-Friendly Control"],
      "center_title": true
    },
    {
      "title": "Who Is It For?",
      "color": "emerald",
      "icon_path": "M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z",
      "subtitle": "Complex, But Powerful",
      "points": ["Large Learning Curve", "Senior Engineers"],
      "extra_margin": true
    }
  ]'
```

## Visual Features
- Grid layout that adapts to 2-4 columns
- Cards with gradient backgrounds and shadows
- Colored icons with customizable SVG paths
- Progressive reveal animation (v-clicks)
- Consistent typography and spacing

## Icon Resources
You can find SVG paths for icons at:
- [Heroicons](https://heroicons.com/)
- [Tabler Icons](https://tabler-icons.io/)
- [Feather Icons](https://feathericons.com/)

## Notes
- Each section appears one at a time with click animations
- Colors should be valid Tailwind color names
- The grid automatically adjusts based on the number of sections