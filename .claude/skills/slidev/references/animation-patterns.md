# Animation Patterns Reference

## Why $clicks Instead of v-click Directives

Slidev's `<v-click>` and `<v-clicks>` directives have a **hydration bug**: on initial page load or reload, elements wrapped in `<v-click>` may briefly flash visible before being hidden. This creates a jarring visual glitch during presentations.

The `$clicks` reactive variable avoids this entirely because `v-if` removes elements from the DOM — there is nothing to flash.

**Rule: Always use `$clicks`-based `v-if` for all click-driven animations. Never use `<v-click>`, `<v-clicks>`, or `v-click` directives.**

## Required Setup

Every slide with click animations MUST have `clicks: N` in frontmatter, where N is the total number of click states:

```yaml
---
clicks: 3
---
```

## Three Animation Patterns

### 1. Additive Reveal

Content appears on click and **stays visible**. The most common pattern.

**When to use**: Sequential lists, card grids, bullet points — anything where items accumulate.

```html
<!-- First section always visible -->
<div class="section">Always visible content</div>

<!-- Appears at click 1, stays visible -->
<div v-if="$clicks >= 1" class="section">Second item</div>

<!-- Appears at click 2, stays visible -->
<div v-if="$clicks >= 2" class="section">Third item</div>
```

**Real example** (column-cards pattern):
```yaml
---
clicks: 3
---
```
```html
<div class="grid grid-cols-3 gap-6">
  <div v-if="$clicks >= 1" class="card">Card 1</div>
  <div v-if="$clicks >= 2" class="card">Card 2</div>
  <div v-if="$clicks >= 3" class="card">Card 3</div>
</div>
```

### 2. Scene Replacement

Content appears at one click and **disappears** at a later click. Used for step-by-step walkthroughs where each scene replaces the previous one.

**When to use**: Multi-step explanations, wizard-style flows, before/after comparisons.

```html
<div class="relative min-h-96">
  <!-- Scene 1: visible only at click 1 -->
  <div v-if="$clicks >= 1 && $clicks < 2" class="absolute inset-0">
    Scene 1 content
  </div>

  <!-- Scene 2: visible only at click 2 -->
  <div v-if="$clicks >= 2 && $clicks < 3" class="absolute inset-0">
    Scene 2 content
  </div>

  <!-- Scene 3: visible from click 3 onward (last scene stays) -->
  <div v-if="$clicks >= 3" class="absolute inset-0">
    Scene 3 content
  </div>
</div>
```

**Key details**:
- Use `absolute inset-0` positioning so scenes stack in the same space
- The last scene typically uses `$clicks >= N` (no upper bound) so it persists
- See `to_add/08-how-skills-work.md` for a complete 7-scene example

### 3. Reactive Styling

Element stays visible but **changes appearance** based on click state. Used for emphasis/de-emphasis effects.

**When to use**: Fading out earlier items when a new one appears, highlighting the current step, progressive styling changes.

```html
<div
  v-if="$clicks >= 1"
  class="card"
  :class="{ 'opacity-40': $clicks >= 3 }"
  style="transition: opacity 0.5s;"
>
  This card appears at click 1, then fades at click 3
</div>
```

**Key details**:
- Use `:class` binding with `$clicks` conditions (NOT `$slidev.nav.clicks`)
- Add `style="transition: opacity 0.5s;"` for smooth visual transitions
- Can combine with additive reveal (`v-if` + `:class` on the same element)

## Pattern Selection Guide

| Use Case | Pattern | Example |
|----------|---------|---------|
| Items appear one by one and stay | Additive | Cards, bullet lists, grid items |
| Step-by-step walkthrough | Scene Replacement | Tutorial steps, flow diagrams |
| Earlier items fade when new ones appear | Additive + Reactive | Continuum with middle emphasis |
| Content cycles through states | Scene Replacement | Before/after, A vs B |
| Non-sequential reveal order | Additive (custom numbering) | DOM order differs from click order |

## Mixing Patterns

Patterns can be combined on the same slide. A common combination is **additive + reactive**:

```html
<!-- Appears at click 1, fades at click 3 -->
<div
  v-if="$clicks >= 1"
  :class="{ 'opacity-40': $clicks >= 3 }"
  style="transition: opacity 0.5s;"
>
  Left extreme
</div>

<!-- Appears at click 2, fades at click 3 -->
<div
  v-if="$clicks >= 2"
  :class="{ 'opacity-40': $clicks >= 3 }"
  style="transition: opacity 0.5s;"
>
  Right extreme
</div>

<!-- Appears at click 3 (the emphasis target) -->
<div v-if="$clicks >= 3">
  The sweet spot (highlighted by contrast)
</div>
```

## Non-Sequential Reveal Order

When DOM order differs from desired click order, simply assign click numbers that match the reveal sequence, not the DOM position:

```html
<!-- In DOM: left, center, right -->
<!-- Reveal order: left (1), right (2), center (3) -->
<div v-if="$clicks >= 1">Left</div>
<div v-if="$clicks >= 3">Center (appears last)</div>
<div v-if="$clicks >= 2">Right (appears second)</div>
```

## Implementation Checklist

When adding click animations to any slide:

1. **Add `clicks: N` to frontmatter** — N = total number of click states
2. **Use `v-if="$clicks >= N"`** — never `<v-click>` or `<v-clicks>`
3. **Use `$clicks`** — never `$slidev.nav.clicks`
4. **Never add `.slidev-vclick-hidden` styles** — not needed with v-if approach
5. **Add transitions via inline style** — `style="transition: opacity 0.5s;"` for reactive styling
6. **Test by reloading the slide page** — verify no flash on initial load
