# wstanza

*Semantic composition for Webflow projects*

---

**wstanza** is a methodology for structuring Webflow projects.
It introduces semantic anchors at critical levels—section, container, and block—while preserving creative freedom inside those blocks. It’s inspired by Blocktail methodology. 

The idea is similar to poetry: stanzas provide rhythm and structure, but the words within remain flexible.
wstanza applies the same principle to Webflow: enough structure to scale, without interfering with Webflow’s native design workflow.

Unlike frameworks, wstanza doesn’t ship with a utility library or replace Webflow’s tools. Instead, it aligns with **Webflow Variables, the Designer panel, and CMS features**, providing a thin semantic layer where it matters most.

---

## The Problem

### When Frameworks Fill Gaps

Before Webflow Variables went mainstream, frameworks emerged that layered their own utility libraries on top of Webflow. These systems attempted to provide reusable spacing, typography, and layout patterns.

The challenge is that this created a **dual system of style management**:

* One layer inside the framework’s utility classes.
* Another layer inside Webflow’s own classes and style panel.

Developers ended up defining and maintaining CSS in two places, often duplicating effort.

### The Class Proliferation Problem

```html
<!-- Example output from a framework-driven approach -->
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

This pattern introduces several problems in Webflow projects:

1. **Selector Complexity** — Components may require 15–20 classes for simple styling. HTML becomes configuration rather than markup.
2. **Platform Bypass** — Styles are locked into class names instead of being managed through Webflow’s style panel.
3. **Stylesheet Bloat** — Frameworks often ship hundreds of classes that go unused in a specific project. Since Webflow has no purge step, they remain indefinitely.
4. **Maintenance Drift** — When conventions evolve, projects must reconcile old and new class patterns.
5. **Overlapping Systems** — Teams manage both Webflow’s classes and the framework’s utilities, leading to confusion and redundancy.

### The Architecture Mismatch

Frameworks of this kind made sense when Webflow lacked **native Variables**. They offered token-like consistency at a time when Webflow didn’t.

Now, Webflow Variables provide:

* **Tokenized values** (sizes, colors, spacing, typography).
* **Visual editing** for those tokens.
* **Consistency** across breakpoints and themes.

With Variables in place, layering an external framework on top often creates more friction than benefit. The need for a separate utility system has largely diminished.

---

## Core Philosophy

### Frontloaded Discipline

wstanza enforces structure **only at the top three levels**:

1. **Section (`sec-`)** → Defines page rows.
2. **Container (`con-`)** → Establishes layout boundaries.
3. **Block (`block-`)** → Marks semantic content units.

Inside blocks? No restrictions. Webflow’s generated classes, one-offs, or CMS-driven selectors all remain valid.
The three anchors are sufficient to keep projects consistent and parseable without constraining design.

### Typography Tokens

The one exception is typography.
The `style-` prefix provides reusable tokens for text (headings, paragraphs, labels, inputs). These tie directly into Webflow Variables and help prevent uncontrolled style proliferation.

---

## Core Concepts

| Prefix   | Scope / Element           | Purpose                                  | Example (Valid)                           |
| -------- | ------------------------- | ---------------------------------------- | ----------------------------------------- |
| `sec-`   | Section (`<section>`)     | Defines page rows / major layout anchors | `<section class="sec-hero">…</section>`   |
| `con-`   | Container (`<div>`)       | Layout wrapper inside a section          | `<div class="con-main">…</div>`           |
| `block-` | Div Block (semantic unit) | Marks a content component                | `<div class="block-feature_card">…</div>` |
| `style-` | Text elements only        | Reusable typography tokens (Variables)   | `<h2 class="style-heading_xl">Title</h2>` |

---

## Valid Patterns

✅ Correct usage of `sec-`, `con-`, and `block-`:

```html
<section class="sec-hero">
  <div class="con-main">
    <div class="block-hero_content">
      <h1 class="style-heading_xl">Welcome</h1>
      <p class="style-text_lead">Lead paragraph</p>
    </div>
  </div>
</section>
```

✅ Nested blocks are allowed:

```html
<div class="block-testimonial_carousel">
  <div class="block-testimonial_card">
    <p class="style-quote">"Great product!"</p>
  </div>
</div>
```

---

## Invalid Patterns

| Pattern                                                 | Issue                                    | Correct Form                                                                        |
| ------------------------------------------------------- | ---------------------------------------- | ----------------------------------------------------------------------------------- |
| `<section class="sec-hero"><div class="block-content">` | Missing `con-` between section and block | `<section class="sec-hero"><div class="con-main"><div class="block-content">`       |
| `<div class="con-wrapper"><div class="content">`        | Container outside a section              | `<section class="sec-wrapper"><div class="con-wrapper"><div class="block-content">` |
| `<div class="block-card"><div class="con-inner">`       | Container placed inside block            | Containers must be first child of section                                           |
| `<div class="style-wrapper">`                           | Misuse of `style-` prefix                | `style-` is for text elements only (`<h1 class="style-heading_xl">`)                |

---

## Quick Reference

```plaintext
STRUCTURE (Required):
sec-[name]    → Section
  con-[name]  → Container (first child)
    block-[name] → Semantic unit
      [Any classes allowed inside]

TYPOGRAPHY (Optional):
style-[token] → Text elements only
```


---

## Advanced Applications

### Observer and Agent Integration

Because wstanza introduces stable anchors (`sec-`, `con-`, `block-`), it also creates predictable points for behavior attachment.

```html
<section class="sec-products">
  <div class="con-grid">
    <div class="block-product_card" 
         data-observer="ProductObserver"
         data-agent="LazyLoad">
      <!-- Block-level behavior -->
    </div>
  </div>
</section>
```

* **Data Observers** provide block-level awareness: lifecycle, events, state.
* **Data Agents** apply behaviors across multiple blocks or contexts.

This approach ensures that automation, animation, and AI-driven workflows can reliably target semantic units without ambiguity.

For a deeper dive into how Observers and Agents work, see [Blocktail Behavioral Patterns](https://blocktail.dev/fundamentals/behavioral-patterns).


