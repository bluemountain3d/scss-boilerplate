# SCSS Boilerplate

A modular, well-structured SCSS architecture designed for scalability, maintainability, and performance. This boilerplate provides a solid foundation for consistent styling across projects of any size.

## 📂 File Structure

```
scss/
├── TEMPLATE/                    # Module templates
│   └── MODULE-TEMPLATE.scss
├── abstracts/                   # Tools and helpers
│   ├── functions/               # SCSS functions
│   │   ├── _fn-[name].scss
│   │   └── index.scss
│   ├── mixins/                  # SCSS mixins
│   │   ├── _mx-[name].scss
│   │   └── index.scss
│   └── variables/               # SCSS variables
│       ├── _var-[name].scss
│       └── index.scss
├── vendors/                     # Third party styles
│   └── index.scss
├── utilities/                   # Utility classes
│   └── index.scss
├── themes/                      # Theme-specific styles
│   └── index.scss
├── base/                        # Base element styles
│   └── index.scss
├── components/                  # UI components
│   └── index.scss
├── layout/                      # Layout components
│   └── index.scss
├── pages/                       # Page-specific styles
│   └── index.scss
└── style.scss
```

## 🚀 Getting Started

1. Copy this boilerplate into your project
2. Customize the variables in `abstracts/variables/` to match your design requirements
3. Add your project-specific styles to the appropriate folders
4. Import the main `style.scss` file in your project

## 🧩 Architecture Overview

This boilerplate follows the principles of ITCSS (Inverted Triangle CSS) and SMACSS (Scalable and Modular Architecture for CSS), with a focus on:

- **Modularity**: Each file has a single responsibility (SRP)
- **Reusability**: Leveraging functions and mixins for consistent patterns
- **Maintainability**: Organized structure with clear naming conventions
- **Performance**: Optimized compilation with minimal duplication

## 📦 Module System

Each module follows a consistent pattern:

```scss
/// @group [FOLDER NAME]
/// @name <MODULE NAME>
///
/// Description of the module's purpose
/// on multiple lines if neccesary
/// =======================

@use '../abstracts/variables/__index__' as var;
@use '../abstracts/functions/__index__' as fn;
@use '../abstracts/mixins/__index__' as mx;

@use 'sass:color';
@use 'sass:list';
@use 'sass:map';
@use 'sass:math';
@use 'sass:meta';
@use 'sass:selector';
@use 'sass:string';

// Module local variables
// $_variable-name: value;

// Module styles
// selector {
//   ...
// }
```

## 🛠️ Key Features

### Responsive System

The boilerplate includes a robust responsive system with:

- **Fluid typography**: Font sizes that scale smoothly across viewport sizes
- **Flexible containers**: Various container types with responsive padding
- **Advanced media queries**: Well-documented mixins with breakpoint handling
- **Container queries**: Support for element-based responsive behavior

Feal free to use it and extend it or remove and start over.

#### Breakpoints

abstracts/

```scss
$breakpoints: (
  'xs': 320px,
  // Extra small
  'mobile': 320px,
  // Semantic alias for xs
  'sm': 540px,
  // Small
  'phablet': 540px,
  // Semantic alias for sm
  'md': 720px,
  // Medium
  'tablet': 720px,
  // Semantic alias for md
  'lg': 1350px,
  // Large
  'laptop': 1350px,
  // Semantic alias for lg
  'xl': 1800px,
  // Extra large
  'desktop': 1800px // Semantic alias for xl,
);
```

#### Media Query Usage

```scss
// Laptop and up
@include for-breakpoint('laptop-up') {
  .container {
    max-width: 80%;
  }
}

// Up to Laptop, all the tablet range and down
@include for-breakpoint('tablet-down') {
  .container {
    max-width: 90%;
  }
}

// Only mobile devices
@include for-breakpoint('mobile-only') {
  .sidebar {
    display: none;
  }
}

// With orientation - tablet and larger in landscape
@include for-breakpoint('tablet-up', 'landscape') {
  .header {
    height: 15vh;
  }
}

// Ultra-wide screens (2:1 aspect ratio)
@include for-ultra-wide {
  .content {
    width: 70%;
  }
}
```

### Unit Conversion

A comprehensive set of functions for converting between different CSS units:

```scss
// Examples
pxToRem(32) => 2rem
remToPx(2) => 32px
pxToPt(20) => 15pt
ptToPx(12) => 16px
remToPt(1.5) => 18pt
ptToRem(24) => 2rem
```

### Color Management

The boilerplate includes a flexible theming system with light and dark mode support:

```scss
// Light theme example
@mixin themeLight {
  --color-primary: #3a86ff;
  --color-secondary: #8ecae6;
  --color-accent: #fb5607;
}

// Dark theme example
@mixin themeDark {
  --color-primary: #4361ee;
  --color-secondary: #3f37c9;
  --color-accent: #f72585;
}
```

Color utilities:

```scss
// Convert hex to RGB string
hexToRgb(#ff0000) => "255, 0, 0"

// Usage in rgba()
background-color: rgba(#{hexToRgb(#0000ff)}, 0.5);
```

### Typography System

A comprehensive typography system with fluid scaling:

```scss
:root {
  // Base font sizes and fluid scaling
  --fs-base: 1rem;
  --fs-clamp: clamp(1rem, 0.7642rem + 1.0142vw, 1.25rem);

  // Heading size scale
  --fs-100: calc(var(--fs-clamp) * 0.75); // 12px at 16px base
  --fs-200: calc(var(--fs-clamp) * 0.875); // 14px at 16px base
  --fs-300: calc(var(--fs-clamp) * 1); // 16px at 16px base
  --fs-400: calc(var(--fs-clamp) * 1.5); // 24px at 16px base
  --fs-500: calc(var(--fs-clamp) * 2); // 32px at 16px base
  // ... and more
}
```

Generate your own `clamp()` using [Utopia Type](https://utopia.fyi/type/calculator/?c=360,16,1.25,1440,20,1.333,0,0,540-720-960-1350-1920-2560&s=0.75|0.5|0.25,1.5|2|3|4|6,s-l&g=s,l,xl,12)

Usage classes:

```scss
// Heading classes
.heading-xl, .heading-lg, .heading-md, .heading-sm, .heading-xs

// Text classes
.text-xl, .text-lg, .text-md, .text-sm, .text-xs

// Special text styles
.lead-in, .caption, .quote

// Title groups
.title-group-xl, .title-group-lg, .title-group-md
```

### Layout System

A flexible container system:

```scss
// Base container with container queries support
.container {
  container-type: inline-size;
  width: 100%;
}

// Boxed container with max-width and responsive padding
.container-boxed {
  max-width: 90rem; // 1440px at 16px root
  margin-inline: auto;
  padding-inline: clamp(0.75rem, 3.125cqw, 2.8125rem);
}

// Narrow container for improved readability
.container-narrow {
  max-width: 72rem; // 1152px at 16px root
  margin-inline: auto;
  padding-inline: clamp(0.75rem, 3.125cqw, 2.8125rem);
}
```

### Spacing System

A consistent spacing system based on typography:

```scss
:root {
  // Extra small spacing
  --gap-050: calc(var(--fs-clamp) * 0.25); // 4px at 16px base
  --gap-100: calc(var(--fs-clamp) * 0.5); // 8px at 16px base

  // Base and medium spacing
  --gap-200: calc(var(--fs-clamp) * 1); // 16px at 16px base
  --gap-300: calc(var(--fs-clamp) * 1.5); // 24px at 16px base

  // Large spacing
  --gap-400: calc(var(--fs-clamp) * 2); // 32px at 16px base
  --gap-500: calc(var(--fs-clamp) * 2.5); // 40px at 16px base

  // ... and more
}
```

### Accessibility Features

Built-in accessibility helpers:

```scss
// Visually hidden content (for screen readers)
.visually-hidden { ... }

// Focus styles
a, button, input, ... {
  &:focus-visible { ... }
}

// Reduced motion preferences
@media (prefers-reduced-motion: reduce) { ... }

// High contrast mode support
@media (forced-colors: active) { ... }
```

### SVG Symbol System

A system for efficiently using SVG icons throughout your project:

```html
<!-- Step 1: Add the symbol container to your HTML (once per page) -->
<svg class="svg-symbols" role="none" xmlns="http://www.w3.org/2000/svg">
  <!-- Email Icon -->
  <symbol id="email-icon" viewBox="0 0 100 100">
    <path
      d="M50.1041 66.1426L64.428 51.8205L86.21 73.602H57.5635H42.6448H14L35.7814 51.8205L50.1041 66.1426Z" />
  </symbol>

  <!-- Add more symbols as needed -->
</svg>

<!-- Step 2: Use symbols anywhere in your HTML -->
<svg class="icon" aria-hidden="true">
  <use href="#email-icon"></use>
</svg>
```

With utility classes:

```scss
.icon { ... }
.icon--sm { ... }
.icon--lg { ... }
.icon--xl { ... }
.icon-flip-h { ... }
.icon-flip-v { ... }
.icon-spin { ... }
```

## 📝 Naming Conventions

- **Functions**: `_fn-[name].scss` - Utility functions for calculations and transformations
- **Mixins**: `_mx-[name].scss` - Reusable style patterns that accept parameters
- **Variables**: `_var-[name].scss` - Global configuration values and maps

## 🔍 Best Practices

1. **Use the template file** when creating new modules
2. **Keep files focused** on a single responsibility
3. **Document your code** with comments and examples using SASS Doc
4. **Leverage the abstracts** to maintain consistency
5. **Follow naming conventions** for better organization

## 📦 Included Functionality

### Functions

- Unit conversion (px to rem, rem to px, etc.)
- Color manipulation (hexToRgb)
- Number formatting (toFixed)
- Unit handling (addUnit, stripUnit)
- Percentage to em conversion

### Mixins

- Responsive breakpoints (for-breakpoint)
- Ultra-wide screen handling (for-ultra-wide)

### Utilities

- Accessibility helpers
- CSS Reset
- Spacing system
- Math and viewport constants
- Grid system template

### Themes

- Typography
- Colors
- Fonts

### Layout

- Container system
- Header, Footer, Sidebar templates

## 📚 Further Reading

For more information on SCSS best practices and architecture patterns:

- [Sass Guidelines](https://sass-guidelin.es/)
- [Sass Doc](http://sassdoc.com/annotations/)
- [ITCSS (Inverted Triangle CSS)](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/)
- [SMACSS (Scalable and Modular Architecture for CSS)](http://smacss.com/)
- [BEM (Block Element Modifier)](http://getbem.com/)

## 📄 License

This boilerplate is free to use for personal and commercial projects. Attribution is appreciated but not required.

## 🙏 Acknowledgements

This boilerplate is inspired by various architecture patterns and best practices in the SCSS community.
