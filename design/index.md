---
layout: default
title: Design
permalink: /design/
---

# Design

Tokens and markdown style reference. Placeholder palette — will be replaced once the visual identity is finalized.

## Tokens

<div class="token-grid">
  <div class="token-swatch">
    <div class="token-swatch__color" style="background: var(--bg); border-bottom: 1px solid var(--rule);"></div>
    <div class="token-swatch__label">bg<code>--bg</code></div>
  </div>
  <div class="token-swatch">
    <div class="token-swatch__color" style="background: var(--text);"></div>
    <div class="token-swatch__label">text<code>--text</code></div>
  </div>
  <div class="token-swatch">
    <div class="token-swatch__color" style="background: var(--heading);"></div>
    <div class="token-swatch__label">heading<code>--heading</code></div>
  </div>
  <div class="token-swatch">
    <div class="token-swatch__color" style="background: var(--accent);"></div>
    <div class="token-swatch__label">accent<code>--accent</code></div>
  </div>
  <div class="token-swatch">
    <div class="token-swatch__color" style="background: var(--muted);"></div>
    <div class="token-swatch__label">muted<code>--muted</code></div>
  </div>
  <div class="token-swatch">
    <div class="token-swatch__color" style="background: var(--rule);"></div>
    <div class="token-swatch__label">rule<code>--rule</code></div>
  </div>
  <div class="token-swatch">
    <div class="token-swatch__color" style="background: var(--code-bg); border-bottom: 1px solid var(--rule);"></div>
    <div class="token-swatch__label">code-bg<code>--code-bg</code></div>
  </div>
  <div class="token-swatch">
    <div class="token-swatch__color" style="background: var(--code-text);"></div>
    <div class="token-swatch__label">code-text<code>--code-text</code></div>
  </div>
</div>

**Type** — `--font-body`: Atkinson Hyperlegible, self-hosted (400/700, roman/italic). `--font-mono`: system monospace stack, used for code.

**Layout** — `--measure`: 42rem max content width. `--space`: 1.5rem base rhythm unit.

## Markdown

### Headings

# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

### Paragraph

Regular paragraph text. Atkinson Hyperlegible is designed for low-vision readers, with distinct letterforms and generous spacing. This is a second sentence to show line wrap and measure at the body size.

### Emphasis

Plain text, **bold text**, *italic text*, ***bold italic text***, and `inline code`.

### Links

A [link to an external site](https://example.com) inline in a sentence.

### Lists

Unordered:

- First item
- Second item
  - Nested item
  - Another nested item
- Third item

Ordered:

1. First step
2. Second step
   1. Sub-step
   2. Sub-step
3. Third step

### Blockquote

> A blockquote spans one or more lines, set off with a left rule.
>
> Second paragraph inside the same blockquote.

### Code block

```js
function greet(name) {
  return `Hello, ${name}!`;
}
```

### Table

| Token      | Value     | Used for          |
|------------|-----------|--------------------|
| `--bg`     | `#FDFCFA` | Page background    |
| `--text`   | `#2B2B28` | Body copy          |
| `--accent` | `#2E5CE6` | Links, highlights  |

### Horizontal rule

Above the rule.

---

Below the rule.
