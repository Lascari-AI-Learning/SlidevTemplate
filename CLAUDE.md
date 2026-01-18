# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Slidev presentation about Claude Code. Slidev is a Vue.js-based presentation framework that uses markdown files for slides.

**Live Template URL:** https://lascari-ai-learning.github.io/SlidevTemplate/

## Common Commands

```bash
# Install dependencies (uses pnpm)
npm run install

# Start development server (http://localhost:3030)
npm run dev

# Build for production
npm run build

# Export presentation to PDF/PNG/PNGs
npm run export

# Auto-generate index.md from slides directory
npm run build:slides

# Generate a new slide from a template
npm run generate:slide -- --template=<template-name> --name=<slide-name> [--variable=value ...]

# List all available templates
npm run list:templates

# Show template usage help
npm run template:help
```

## Architecture

### Slide System
- Individual slides are stored as markdown files in `slides/` directory
- Slides are numbered (e.g., `01-about-me.md`, `02-introduction.md`) for automatic ordering
- `scripts/build.ts` generates `index.md` by concatenating all slides in numerical order
- Each slide can have frontmatter for theme and layout configuration

### Key Directories
- `slides/` - Individual slide markdown files with inline templates and styles
- `slide-templates/` - Reusable slide templates with documentation and examples
- `ai_docs/` - AI-related documentation including speaker profile and brand guidelines
- `public/` - Static assets accessible in slides
- `scripts/` - Build and generation scripts

### Theming
- Uses custom fonts: Styrene A (headings) and Styrene B (body text)
- Custom color palette defined in styles
- Light color scheme by default
- Tailwind/Windi CSS for styling

## Slide Template System

### Overview
The project uses a template-based system for creating slides. Instead of using Slidev's built-in Vue layouts, we have a custom template structure that provides:
- Visual examples (screenshots) of each template
- Detailed documentation for each template
- Easy generation of new slides from templates
- Consistent structure across presentations

### Template Structure
Each template is stored in `slide-templates/<template-name>/` with:
```
slide-templates/
├── [template-name]/        # Template for overview/agenda slides
│   ├── slide.md            # The template file with placeholders
│   ├── description.md      # Usage documentation
│   └── preview.png         # Screenshot showing the template
└── ... (other templates)
```

### Available Templates

#### Core Templates (Essential for most presentations)
1. **title** - Opening slide with title, subtitle, and optional QR code
2. **column-cards** - Flexible column layout with icon cards (2-4 columns)
3. **about-me** - Speaker introduction with photo and background
4. **conclusion-lets-connect** - Closing slide with contact QR codes

#### Content Templates
5. **icon-list-content** - Multiple sections with icons and bullet points
6. **continuum-diagram** - Visual spectrum showing items along a gradient

### Using Templates

To generate a new slide from a template:
```bash
npm run generate:slide -- --template=title --name=00-my-title \
  --title="My Presentation" \
  --subtitle="An Amazing Talk" \
  --qr_link="https://example.com" \
  --qr_label="Follow Along"
```

Each template has different variables. Check the template's `description.md` file for:
- Required and optional variables
- Usage examples
- Visual features
- Best practices

### Creating New Templates

To create a new template:
1. Create a new folder in `slide-templates/`
2. Add `slide.md` with the template structure using `{{variable}}` placeholders
3. Write `description.md` with usage instructions
4. Optionally add a `preview.png` screenshot

Template syntax supports:
- Simple variables: `{{title}}`
- HTML variables: `{{{html_content}}}`
- Conditionals: `{{#if variable}}...{{/if}}`
- Loops: `{{#each items}}...{{/each}}`

## Development Workflow

1. Choose a template: `npm run list:templates`
2. Generate a slide: `npm run generate:slide -- --template=<name> --name=<slide-name> [variables]`
3. Edit the generated slide in `slides/` if needed
4. Run `npm run build:slides` to regenerate index.md
5. Use `npm run dev` to preview changes
6. Slides support standard markdown, Vue components, and inline styles

## Deployment
- Configured for both Netlify and Vercel
- Build command: `pnpm build`
- Output directory: `dist`