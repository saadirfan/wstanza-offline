# wstanza
*Semantic scaffolding for Webflow projects*

---

## Introduction

**wstanza** provides a minimal semantic structure for Webflow projects through just two concepts:

* **Context** marks environmental sections
* **Block** defines content units

Inside blocks, you have complete freedom. Webflow's generated classes, custom names, and CMS elements all remain valid.

Inspired by Blocktail methodology but radically simplified for Webflow's visual-first workflow, wstanza gives just enough structure to scale without disrupting the platform's native patterns.

---

## The Problem

### When Frameworks Filled the Gap

Before Webflow Variables became standard, frameworks emerged to provide what Webflow was missing: reusable spacing, typography, and layout patterns. They did this by layering utility libraries on top of Webflow's class system.

While these frameworks accelerated prototyping, they introduced a **dual system of style management**:

* One layer in the framework's utility classes
* Another layer in Webflow's own style panel

The result was duplication and drift. Teams maintained styles in two places, never fully sure which system was "in charge."

### The Class Proliferation Problem

```html
<!-- Framework-driven approach -->
<div class="padding-top-large padding-bottom-medium max-width-medium 
            margin-left-auto margin-right-auto text-align-center 
            background-neutral-100 border-radius-small shadow-medium
            tablet-padding-small mobile-hide desktop-flex">
  <h2 class="heading-size-xxl font-weight-bold text-color-primary 
             line-height-1-2 margin-bottom-small tablet-heading-size-xl 
             mobile-heading-size-large">
    Welcome
  </h2>
</div>
```

This pattern creates recurring issues:

1. **Selector Complexity** – Components require 15–20 classes for basic styling
2. **Platform Bypass** – Styling lives in class names instead of Webflow's style panel
3. **Stylesheet Bloat** – Hundreds of unused utility classes persist indefinitely
4. **Maintenance Drift** – Inconsistent patterns across framework versions
5. **Overlapping Systems** – Managing both Webflow's classes and framework utilities

### The Architecture Mismatch

These frameworks made sense when Webflow lacked Variables. But Webflow has since closed that gap:

* **Variables** now provide tokenized values for spacing, colors, and typography
* **Visual editing** manages tokens directly in the Designer
* **Native responsiveness** handles breakpoints without utility classes

With Variables in place, utility frameworks create redundancy rather than value.

---

## Core Philosophy

### Radical Simplicity

wstanza provides just two semantic anchors:

1. **Context** → Environmental sections (Webflow Section)
2. **Block** → Content units (Webflow Div Block)

Plus typography tokens:

3. **Style** → Reusable text classes connected to Variables

That's it. No mandatory wrappers. No rigid hierarchy. Just enough structure to be useful, not enough to be restrictive.

---

## Core Concepts

### Context

Contexts define environmental sections of your page. They map to Webflow's Section element and can handle their own layout constraints.

```html
<!-- Basic context -->
<section class="context">
  <!-- Content goes here -->
</section>

<!-- Semantic context -->
<section class="context-hero">
  <!-- Hero content -->
</section>

<!-- Context with modifiers -->
<section class="context context-dark">
  <!-- Dark themed section -->
</section>
```

**Context modifiers** provide variations without complexity:
- `context-flushed` – No padding
- `context-small` – Reduced spacing
- `context-dark` – Dark theme
- `context-wide` – Full width

### Block

Blocks are semantic content units that live inside contexts. They map to Webflow's Div Block element.

```html
<!-- Basic block -->
<div class="block">
  <!-- Any content -->
</div>

<!-- Semantic block -->
<div class="block-testimonial">
  <!-- Testimonial content -->
</div>

<!-- Block with Webflow's generated classes -->
<div class="block div-block-47">
  <!-- Mixed approach is fine -->
</div>
```

### Style (Typography)

Typography uses the `style-` prefix for reusable text tokens connected to Webflow Variables.

```html
<h1 class="style-heading_xl">Hero Title</h1>
<h2 class="style-heading_lg">Section Title</h2>
<p class="style-text_lead">Lead paragraph</p>
<p class="style-text_body">Body content</p>
```

Common tokens:
- `style-heading_xl` – Hero headings
- `style-heading_lg` – Section titles
- `style-heading_md` – Subsections
- `style-text_lead` – Lead paragraphs
- `style-text_body` – Body content
- `style-text_small` – Captions
- `style-label` – Form labels

---

## Pattern Examples

### Basic Structure

```html
<section class="context">
  <div class="block">
    <h2 class="style-heading_lg">Welcome</h2>
    <p class="style-text_body">Content goes here</p>
  </div>
</section>
```

### Semantic Naming

```html
<section class="context-hero context-dark">
  <div class="block-hero_content">
    <h1 class="style-heading_xl">Welcome to Our Platform</h1>
    <p class="style-text_lead">Build better websites</p>
  </div>
</section>
```

### Multiple Blocks

```html
<section class="context-features">
  <div class="block-feature_card">
    <h3 class="style-heading_md">Fast</h3>
    <p class="style-text_body">Speed matters</p>
  </div>
  
  <div class="block-feature_card">
    <h3 class="style-heading_md">Simple</h3>
    <p class="style-text_body">Clarity wins</p>
  </div>
</section>
```

### With Layout Constraints

When you need max-width or centering, apply it directly to the context or specific blocks:

```css
/* Context handles its own constraints */
.context {
  max-width: 1200px;
  margin: 0 auto;
  padding: 4rem 2rem;
}

/* Or specific blocks can be constrained */
.block-narrow {
  max-width: 800px;
  margin: 0 auto;
}
```

---

## Quick Reference

```plaintext
STRUCTURE:
context         → Environmental section
  block         → Content unit
    [freedom]   → Any Webflow classes

VARIATIONS:
context-{name}  → Semantic context
block-{name}    → Semantic block
context-{mod}   → Context modifier

TYPOGRAPHY:
style-{token}   → Text elements only
```

---

## Advanced: Behavioral Layer

### Observers and Agents

Once you have stable semantic anchors, they become reliable mount points for behavior:

* **Observers (`data-observer`)** – Provide block-level sovereignty over lifecycle and states
* **Agents (`data-agent`)** – Add reusable behaviors without claiming ownership

```html
<section class="context-products">
  <div class="block-product_card"
       data-observer="ProductObserver"
       data-agent="LazyLoad">
    <!-- Observer manages lifecycle -->
    <!-- Agent adds lazy loading -->
  </div>
</section>
```

This behavioral layer remains optional but provides clear patterns for adding interactivity when needed.

---

## Migration Guide

### From Utility Frameworks

1. **Identify sections** → Add `context` class
2. **Find content units** → Add `block` class
3. **Replace text utilities** → Use `style-` tokens
4. **Move styles to panel** → Let Webflow handle visual properties
5. **Clean up** → Remove utility classes

### From Scratch

1. **Start simple** → Use generic `context` and `block`
2. **Add meaning** → Use semantic names where helpful
3. **Define typography** → Create Variables and `style-` tokens
4. **Stay flexible** → Mix with Webflow's generated classes

---

## Why wstanza?

### For Humans
- **Just 2 concepts** to remember (plus typography)
- **No mandatory nesting** or wrappers
- **Works with** Webflow, not against it
- **Progressive enhancement** – start simple, add specificity as needed

### For AI
- **Stable anchors** survive Webflow republishing
- **Predictable structure** for automation
- **Clear patterns** for prompt-driven development
- **Semantic meaning** improves AI comprehension

### For Scale
- **Minimal overhead** – no framework bloat
- **Variables-first** – leverages Webflow's native features
- **Maintainable** – clear structure without rigidity
- **Portable** – patterns work across projects

---

## Examples in Practice

### Before: Framework Approach
```html
<div class="padding-large max-width-medium center-align 
            bg-gray radius-medium shadow mobile-hide">
  <h2 class="text-xxl bold primary-color">Welcome</h2>
</div>
```

### After: wstanza
```html
<section class="context">
  <div class="block">
    <h2 class="style-heading_lg">Welcome</h2>
  </div>
</section>
```

The styling moves to Webflow's style panel where it belongs, using Variables for consistency.

---

## Common Patterns

### Hero Section
```html
<section class="context-hero context-dark">
  <div class="block-hero_content">
    <h1 class="style-heading_xl">Welcome</h1>
    <p class="style-text_lead">Subtitle text</p>
    <a class="button">Get Started</a>
  </div>
</section>
```

### Feature Grid
```html
<section class="context-features">
  <div class="block-feature_grid">
    <div class="block-feature_card">
      <h3 class="style-heading_md">Feature 1</h3>
    </div>
    <div class="block-feature_card">
      <h3 class="style-heading_md">Feature 2</h3>
    </div>
  </div>
</section>
```

### CMS Integration
```html
<section class="context-blog">
  <div class="block">
    <!-- Webflow Collection List -->
    <div class="w-dyn-list">
      <!-- CMS content -->
    </div>
  </div>
</section>
```

---

## Summary

wstanza simplifies Webflow development to its essence:

1. **Context** → Environmental sections
2. **Block** → Content units  
3. **Style** → Typography tokens

No mandatory wrappers. No utility explosion. Just semantic anchors that make projects maintainable and AI-friendly.

The result: cleaner HTML, better Webflow integration, and sustainable development practices that scale.