# HTML & CSS Code-Along Guide

Starter file to create first:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Code Along</title>
</head>
<body>

  <!-- practice goes here -->

</body>
</html>
```


---

## 1. Semantic HTML

**Exercise:** Build a semantic skeleton for a small "About Me" page — header with your name + nav with 3 fake links, a main section with a heading and a paragraph, a footer. No styling yet, just structure.

---

## 2. Box Model

**Exercise:** Make three boxes side by side (just stack the HTML divs one after another for now, don't worry about layout yet — you'll fix the stacking with flexbox next). Give each a different `padding`, `border`, and `margin` so you can see how the spacing changes. Open dev tools and inspect the box model diagram for one of them.

---

## 3. Flexbox (1D layout — rows/columns)

`display: flex` turns a container's children into a flexible row (default) or column.

**Example:**
```css
.row {
  display: flex;
  justify-content: space-between; /* horizontal spacing */
  align-items: center;            /* vertical alignment */
  gap: 1rem;
}
```
```html
<div class="row">
  <div class="box">1</div>
  <div class="box">2</div>
  <div class="box">3</div>
</div>
```

**Exercise:** Take your three boxes from the box-model exercise, wrap them in a parent div, and:
1. Make them sit in a row with even spacing between them
2. Then try `justify-content: center` and `align-items: flex-start` instead — see what changes
3. Switch `flex-direction: column` and see them stack vertically

---

## 4. Grid (2D layout — rows AND columns)

`display: grid` for actual layout structure, not just a single row.

**Example:**
```css
.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}
```
```html
<div class="gallery">
  <div class="box">1</div>
  <div class="box">2</div>
  <div class="box">3</div>
  <div class="box">4</div>
  <div class="box">5</div>
  <div class="box">6</div>
</div>
```

**Exercise:** Make a 6-box gallery grid. Try:
1. `repeat(3, 1fr)` — 3 even columns
2. Change to `repeat(2, 1fr)` — see it reflow to 2 columns, 3 rows
3. Try `grid-template-columns: 2fr 1fr 1fr` — first column now twice as wide

Flex vs grid rule of thumb: reach for **flex** when aligning a single row/column of things, **grid** when you're laying out a full 2D structure.

---

## 5. Positioning

`relative`, `absolute`, `fixed`, `sticky`.

**Example — a badge stuck to the corner of a card:**
```css
.card {
  position: relative;
  width: 200px;
  height: 120px;
  background: lightyellow;
}
.badge {
  position: absolute;
  top: -10px;
  right: -10px;
  background: tomato;
  color: white;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}
```
```html
<div class="card">
  <div class="badge">3</div>
  Card content
</div>
```

**Exercise:** Build this card + badge exactly as above, then make a `nav` that uses `position: sticky; top: 0;` so it stays pinned when you scroll (you'll need to add enough dummy paragraphs below it to make the page scrollable).

---

## 6. Responsive Units & Media Queries

Prefer `rem` (text), `%`/`vw`/`vh` (layout) over hardcoded `px`. Use media queries to adapt at breakpoints.

**Example:**
```css
.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

@media (max-width: 600px) {
  .gallery {
    grid-template-columns: 1fr;
  }
}
```

**Exercise:** Add this media query to your gallery from exercise 4. Shrink your browser window (or use dev tools' responsive mode) below 600px and watch it collapse to a single column. Then also try `clamp()` on a heading: `font-size: clamp(1.5rem, 5vw, 3rem);` and resize the window to see it scale smoothly.

---

## 7. Visual Polish — this is where "cute" happens

`border-radius`, `box-shadow`, `transition`, `transform`, `@keyframes`.

**Example — a hover-interactive card:**
```css
.cute-card {
  width: 180px;
  padding: 1.5rem;
  border-radius: 20px;
  background: #ffe4ec;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.cute-card:hover {
  transform: scale(1.05) rotate(-1deg);
  box-shadow: 0 8px 20px rgba(0,0,0,0.15);
}
```

**Example — a simple bounce animation:**
```css
.bouncy {
  display: inline-block;
  animation: bounce 1s infinite;
}
@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}
```

**Exercise:**
1. Build the hover card above, then tweak the numbers until it feels "yours" (bigger radius? different rotate direction? bigger shadow?)
2. Put an emoji or a small circle div in a `.bouncy` span and watch it bounce forever
3. Combine them: make the card itself do a subtle bounce on page load using `animation`, then still respond to `:hover` with the transform

---

## 8. CSS Variables + Pseudo-selectors

Custom properties keep a palette consistent and easy to tweak. Pseudo-selectors (`:hover`, `:focus`, `:nth-child()`) target elements by state or position.

**Example:**
```css
:root {
  --main-color: #ff9ecb;
  --bg-color: #fff5f8;
  --radius: 16px;
}
body {
  background: var(--bg-color);
}
.box {
  background: var(--main-color);
  border-radius: var(--radius);
}
.list li:nth-child(odd) {
  background: #f0f0f0;
}
.list li:hover {
  background: var(--main-color);
}
```

**Exercise:** Define 3 CSS variables for a color palette at the top of your stylesheet. Rebuild your gallery/cards using only `var(--...)` for colors — then change just the `:root` values and watch the whole page re-theme itself instantly. Add a `<ul>` with 5 `<li>` items and style odd/even rows differently with `:nth-child()`.

---

## Capstone: Put it all together

Now build one small cute thing using everything above — pick one:
- A little animated character/avatar card with a hover effect and a bounce
- A "mood picker" — a row (flexbox) of emoji buttons that scale up on hover
- A virtual plant/pet card with a grid layout, custom color variables, and a subtle idle animation

Structure it semantically, lay it out with flex or grid, style the box model, add responsive sizing, and finish with the polish layer (radius, shadow, transition, animation).

Come back and show me what you build, or ask if you get stuck on any specific piece.