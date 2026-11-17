---
name: web-typography
description: CSS typography rules for web pages and UI. Use when writing or reviewing HTML/CSS that sets text - tabs and nav with a bold active state, button and badge labels, links, footnotes, headlines, acronyms, quotes, file names, justified or narrow columns, and card titles.
---

# Web typography rules

Apply these when writing or reviewing CSS that sets text. Each rule names the defect, then the fix.

## 1. Reserve bold width

A tab or nav item that goes bold on hover or when active gets wider and shifts the whole row. Reserve the bold width with a hidden bold copy stacked in the same grid cell.

```css
.tab { display: inline-grid; }
.tab > *, .tab::after { grid-area: 1 / 1; }
.tab::after { content: attr(data-text); font-weight: 700; visibility: hidden; }
```

The element needs `data-text` equal to its label.

## 2. Trim the text box

Fonts reserve room for descenders, so a label sits slightly above centre in a button, most visibly in all caps. Trim the text box to cap height and baseline.

```css
.label { text-box-trim: trim-both; text-box-edge: cap alphabetic; }
```

Supported in Chrome 133+ and Safari 18.2+. In other browsers the label renders as before, so the rule is safe to ship.

## 3. Offset underlines

The default underline cuts through descenders such as g and y. Push it below them.

```css
a { text-underline-offset: 0.2em; }
```

## 4. Superscripts that keep line spacing even

A default `sup` makes its line taller than the others. Take it out of the line-height calculation.

```css
sup { line-height: 0; position: relative; vertical-align: baseline; top: -0.5em; }
```

## 5. Fluid type

A headline with a fixed size per breakpoint jumps at each breakpoint. Scale it with `clamp`.

```css
h1 { font-size: clamp(2rem, 1rem + 5vw, 4rem); }
```

Keep a `rem` term in the middle value so the size still responds to user zoom.

## 6. Small caps for acronyms

Acronyms in full caps (CRM, REST API, CSV, PDF) read as shouting inside body text. Mark them up with `abbr` and set them in small caps.

```css
abbr { font-variant-caps: all-small-caps; }
```

## 7. Curly quotes

Straight quotes and apostrophes (`"this"`, `don't`) look mechanical. Use curly ones (“this”, don’t). This is a change to the text itself. No CSS property does it.

## 8. Middle truncation for file names

Truncating a file name at the end hides the extension and the part that distinguishes similar files. Split the name and the extension into two elements and truncate only the name.

```css
.file { display: flex; }
.name { overflow: hidden; text-overflow: ellipsis; white-space: nowrap; min-width: 0; }
.ext  { flex-shrink: 0; }
```

## 9. Auto hyphenation

Justified text in a narrow column leaves large gaps between words. Let the browser hyphenate. It needs the document language.

```html
<html lang="en">
```
```css
p { hyphens: auto; }
```

## 10. Line-clamped titles

Titles of different lengths give a row of cards different heights. Clamp the title to a fixed number of lines.

```css
h3 { display: -webkit-box; -webkit-box-orient: vertical; -webkit-line-clamp: 2; overflow: hidden; }
```

Source: "10 Niche Typography Hacks", TikTok @charles.unemployed.
