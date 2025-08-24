# wstanza

*Semantic composition for Webflow projects*


**wstanza** is a lightweight methodology for organizing Webflow projects.
It introduces predictable class prefixes at the section, container, and block level while leaving freedom inside blocks.
This gives teams a consistent structure, keeps Webflow’s Designer workflow intact, and provides semantic anchors for automation or AI parsing.



1. **Minimal Structure** — Enforce discipline only at three levels:

   * `sec-` → Section (page row)
   * `con-` → Container (layout wrapper)
   * `block-` → Content unit

2. **Freedom Inside Blocks** — Classes inside `block-` elements can be anything (Webflow-generated, one-offs, CMS-driven).

3. **Optional Typography Tokens** — Use `style-` classes for text elements to create reusable typography linked to Webflow Variables.

---

## The Four Prefixes

| Prefix   | Scope              | Purpose               | Rules                                                |
| -------- | ------------------ | --------------------- | ---------------------------------------------------- |
| `sec-`   | Section            | Defines page rows     | Always applied to Webflow Sections                   |
| `con-`   | Container          | Layout constraints    | First child of a section                             |
| `block-` | Div Block          | Semantic content unit | First child of a container; inside = freeform        |
| `style-` | Text elements only | Typography tokens     | Applied only to headings, paragraphs, labels, inputs |

---

## Composition Pattern

```plaintext
sec-[name]      → Section
  con-[name]    → Container
    block-[name] → Semantic unit
      [Any class names allowed here]
```

**Rules:**

* Every section (`sec-`) must contain a container (`con-`).
* Every container (`con-`) must contain a block (`block-`).
* Inside blocks, naming is unrestricted.
* `style-` is optional and applies only to text elements.

---

## Examples

### Hero Section

```html
<section class="sec-hero">
  <div class="con-main">
    <div class="block-hero_content">
      <h1 class="style-heading_xl">Welcome</h1>
      <p class="intro-text">Complete freedom inside blocks</p>
      <a class="button w-button">Get Started</a>
    </div>
  </div>
</section>
```

### CMS Blog List

```html
<section class="sec-blog">
  <div class="con-content">
    <div class="block-post_grid">
      <div class="w-dyn-list">
        <div class="w-dyn-item">
          <h2 class="style-heading_md">Blog Title</h2>
          <p class="excerpt">Description</p>
        </div>
      </div>
    </div>
  </div>
</section>
```

---

## Typography Tokens

`style-` tokens provide reusable, variable-driven text styles:

```html
<h1 class="style-heading_xl">Title</h1>
<p class="style-text_lead">Lead paragraph</p>
<label class="style-form_label">Email</label>
```

* Connects directly to Webflow Variables (sizes, colors, fonts).
* Keeps typography consistent across the project.
* Only applied to text elements.

---

## Invalid Patterns

| Example                                                 | Issue                        | Fix                              |
| ------------------------------------------------------- | ---------------------------- | -------------------------------- |
| `<section class="sec-hero"><div class="block-content">` | Missing container            | Add `con-`                       |
| `<div class="con-wrapper"><div class="content">`        | Container not inside section | Wrap with `sec-`                 |
| `<div class="block-card"><div class="con-inner">`       | Container inside block       | Containers only at section level |
| `<div class="style-wrapper">`                           | Misused `style-`             | Use only on text                 |

---

## Quick Reference

```plaintext
STRUCTURE (Required):
sec-[name]    → Section
  con-[name]  → Container
    block-[name] → Content unit
      [Anything goes]

TYPOGRAPHY (Optional):
style-[token] → Text elements only
```

---

## Key Takeaways

* Use **`sec-`, `con-`, `block-`** for structure.
* Use **`style-`** only for text elements.
* Keep everything else free-form inside blocks.
* This system fits on a single note:

```plaintext
sec → con → block → [freedom]
         └── style- (text only)
```

