---
name: ui-polish
description: CSS rules for visual polish in web UI. Use when writing or reviewing HTML/CSS for nested rounded corners, borders on coloured surfaces, colour palettes, gradients, icons beside text, carousels and scroll areas, icon swap transitions, dark mode elevation, full-height mobile sections, and product images on tinted backgrounds.
---

# UI polish rules

Apply these when writing or reviewing CSS for layout, colour and motion. Each rule names the defect, then the fix.

## 1. Concentric radius

A rounded element inside a rounded container looks wrong when both use the same radius. Inner radius = outer radius minus the padding between them.

```css
.outer { border-radius: 48px; padding: 18px; }
.inner { border-radius: calc(48px - 18px); }
```

## 2. Alpha borders

A solid grey border (`#e4e4e7`) looks pasted on when the surface behind it is coloured. Use a translucent border so it blends into any surface.

```css
border-color: rgb(0 0 0 / 0.12);
```

On dark surfaces use white at a low alpha.

## 3. OKLCH palettes

HSL colours at the same lightness value look unequally bright (yellow and green look lighter than blue and violet). Build palettes in OKLCH, where equal L looks equal.

```css
background: oklch(76% var(--c) var(--h));
```

## 4. OKLCH gradients

A gradient between two distant hues goes grey in the middle when interpolated in sRGB. Interpolate in OKLCH.

```css
background: linear-gradient(90deg in oklch, #2563eb, #f59e0b);
```

## 5. Match icon weight to text weight

A thin icon beside bold text looks mismatched. Set the icon stroke so its drawn thickness equals the stem thickness of the text next to it. In the example, a 1px stroke drew at 1.5px beside 3.9px stems, and `stroke-width: 2.6` matched them.

```css
svg { stroke-width: 2.6; }
```

Measure for the font and size in use. 2.6 is the value for that example.

## 6. Masked edges

A carousel or scroll area that cuts items off with a hard edge looks sliced. Fade the edges with a mask, which works on any background.

```css
.carousel { mask: linear-gradient(90deg, #0000, #000 15% 85%, #0000); }
```

## 7. Blurred icon swaps

When one icon replaces another (copy to check), a plain opacity crossfade shows both icons at once. Add a small blur to the outgoing icon so the swap reads as one shape.

```css
.out { opacity: 0; filter: blur(4px); }
```

## 8. Dark mode depth

Shadows barely show on dark backgrounds, so they cannot signal elevation there. Use lightness: the higher the layer, the lighter its background. Page darkest, card lighter, menu lightest.

```css
.page { background: #141417; }
.menu { background: #2d2d33; }
```

## 9. Dynamic viewport units

`100vh` on mobile Safari is taller than the visible area, so content at the bottom hides under the toolbar. Use `dvh`.

```css
.hero { height: 100dvh; }
```

## 10. Multiply blending for product images

A product photo with a white background shows a white box on a tinted card. Multiply blending makes the white disappear.

```css
img { mix-blend-mode: multiply; }
```

This only works on light backgrounds. On dark backgrounds use a transparent image.

Source: "10 Niche Design Hacks", TikTok @charles.unemployed.
