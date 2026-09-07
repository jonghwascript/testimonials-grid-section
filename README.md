# Frontend Mentor - Testimonials grid section solution

This is a solution to the [Testimonials grid section challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/testimonials-grid-section-Nnw6J7Un7). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Concepts I studied](#concepts-i-studied)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
  - [AI Collaboration](#ai-collaboration)
  - [Questions for feedback](#questions-for-feedback)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the site depending on their device's screen size

### Screenshot

![Desktop Design](.screenshot.jpg)

### Links

- Solution URL: [Repository](https://github.com/jonghwascript/testimonials-grid-section.git)
- Live Site URL: [Live site](https://jonghwascript.github.io/testimonials-grid-section)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- CSS Grid with `grid-template-areas`
- Mobile-first workflow
- Google Fonts (Barlow Semi Condensed)

### What I learned

#### 1. Responsive Grid Layout with `grid-template-areas`

Using named grid areas makes complex responsive layouts intuitive and maintainable. Each breakpoint can completely restructure the layout by redefining the areas.

```css
/* Mobile: Single column stack */
.testimonials-grid {
  display: grid;
  grid-template-columns: minmax(0, 305px);
  gap: 2rem;
}

/* Tablet: 2-column layout */
@media (min-width: 48rem) {
  .testimonials-grid {
    grid-template-columns: repeat(2, 1fr);
    grid-template-areas:
      "student1 student1"
      "student2 student3"
      "student4 student4"
      "student5 student5";
  }
}

/* Desktop: 4-column asymmetric layout */
@media (min-width: 64rem) {
  .testimonials-grid {
    grid-template-columns: repeat(4, 1fr);
    grid-template-areas:
      "student1 student1 student2 student5"
      "student3 student4 student4 student5";
  }
}
```

#### 2. Flexbox for Card Internal Layout

Each testimonial card uses Flexbox for simple vertical stacking with consistent spacing.

```css
.testimonial {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding: 2rem;
  border-radius: 8px;
}
```

#### 3. CSS Custom Properties for Design Tokens

Centralized color and typography management using CSS variables.

```css
:root {
  --purple-500: #7541c8;
  --grey-500: #48556a;
  --font-body: "Barlow Semi Condensed", sans-serif;

  /* Font shorthand: weight | size/line-height | family */
  --text-preset-1: 600 1.25rem/1.2 var(--font-body);
}

.testimonial__reviews {
  font: var(--text-preset-1);
}
```

#### 4. Natural Word Breaking for Long English Words

```css
.testimonial__reviews,
.testimonial__career-journey {
  overflow-wrap: break-word;
}
```

This ensures long words break naturally instead of overflowing their containers.

### Concepts I studied

These are CSS Grid concepts I researched during this project but didn't implement in the final solution.

#### CSS Subgrid for Cross-Card Alignment

When cards have varying text lengths but you want consistent positioning (e.g., author info always at the bottom), CSS Subgrid can align content across sibling elements.

```css
/* Mobile: Basic Flexbox */
.testimonial-item {
  display: flex;
  flex-direction: column;
}

/* Desktop: Subgrid for perfect row alignment */
@media (min-width: 768px) {
  .testimonial-container {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(3, auto); /* Must match child's span */
  }

  .testimonial-item {
    grid-row: span 3;
    display: grid;
    grid-template-rows: subgrid;
  }
}
```

**Critical Rule**: The number of rows a child spans must equal the parent's explicit row count.

- **Works**: Parent has 3+ rows, child uses `span 3` → child gets 3 internal rows
- **Breaks**: Parent has 2 rows, child requests `span 3` → browser creates implicit rows, breaking layout

#### Content-Length Based Layout Positioning

**Pure CSS Grid cannot position items based on content length.** CSS adjusts box sizes but can't make logical decisions like "long text goes to column 2."

**Workaround 1: JavaScript class assignment**

```css
.item { grid-column: span 1; }
.item.is-long { grid-column: span 2; }
```

**Workaround 2: Tetris-style packing**

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-flow: dense; /* Fills gaps automatically */
}
```

This creates Pinterest-style layouts where smaller items fill empty spaces.

### Continued development

Areas I want to focus on in future projects:

- CSS Subgrid for aligning content across sibling elements
- CSS Container Queries for component-based responsive design
- Advanced `grid-template-areas` patterns

### Useful resources

- [MDN - CSS Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout) - Comprehensive guide to CSS Grid
- [MDN - grid-template-areas](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-areas) - Named grid areas documentation
- [MDN - Subgrid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Subgrid) - Understanding subgrid behavior
- [CSS Tricks - A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/) - Visual reference for grid properties

### AI Collaboration

- **Tools used**: Claude Code (Anthropic)
- **How I used it**:
  - Understanding CSS Grid, `grid-template-areas`, and Subgrid concepts
  - Learning about content-length based layout limitations
  - Writing and reviewing documentation
- **What worked well**: Claude helped explain complex CSS Grid concepts (especially Subgrid parent-child relationships) and assisted with README documentation
- **What didn't**: Had to verify responsive breakpoints manually in the browser

## Author

- Frontend Mentor - [@jonghwascript](https://www.frontendmentor.io/profile/jonghwascript)
