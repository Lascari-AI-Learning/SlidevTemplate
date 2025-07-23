# Welcome to [Slidev](https://github.com/slidevjs/slidev)!

To start the slide show:

- `pnpm install`
- `pnpm dev`
- visit <http://localhost:3030>

Edit the markdown files in the [slides](./slides/) directory to see the changes.

Learn more about Slidev at the [documentation](https://sli.dev/).

## Building Slides

To build all slides in the `slides/` directory:

```bash
pnpm build:slides
```

This will:
- Build each `.md` file in the `slides/` directory
- Output the built slides to the `dist/` directory
- Generate an index page with links to all slides
