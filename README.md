# SCSS Boilerplate Documentation

This document explains the SASS 7-1 folder structure, organized for modularity, scalability, and maintainability. Each folder serves a specific purpose, helping to separate concerns and speed up development.

## Directory Structure example:
```plaintext
scss/
├── TEMPLATE/                    # Module templates
│   └── __MODULE-TEMPLATE__.scss
├── abstracts/                   # Tools and helpers
│   ├── functions/               # SCSS functions
│   │   ├── _fn-[name].scss
│   │   └── _index.scss
│   ├── mixins/                  # SCSS mixins
│   │   ├── _mx-[name].scss
│   │   └── _index.scss
│   └── variables/               # SCSS variables
│       ├── _var-[name].scss
│       └── _index.scss
├── vendors/                     # Third party styles
│   ├── _modern-reset.scss
│   └── _index.scss
├── utilities/                   # Utility classes
│   ├── _reset.scss
│   ├── _math-viewport.scss      # Math constants and viewport units
│   ├── _a11y-helpers.scss       # Accessibility helpers
│   ├── _spacing.scss            # Spacing properties and utilities
│   ├── _grid.scss               # Grid system
│   └── _index.scss
├── themes/                      # Theme-specific styles
│   ├── _font-faces.scss         # Custom font declarations
│   ├── _colors.scss             # Color custom properties
│   ├── _typography.scss         # Typography custom properties
│   └── _index.scss
├── base/                        # Base element styles
│   ├── _html.scss
│   ├── _body.scss
│   ├── _main.scss
│   ├── _form.scss
│   └── _index.scss
├── components/                  # UI components
│   ├── _button.scss
│   ├── _carousel.scss
│   └── _index.scss
├── layout/                      # Layout components
│   ├── _container.scss
│   ├── _header.scss
│   ├── _footer.scss
│   └── _index.scss
├── pages/                       # Page-specific styles
│   ├── _home.scss
│   ├── _about.scss
│   └── _index.scss
└── style.scss                   # Main file
```

## Detailed Folder Explanations
### TEMPLATE Directory
The TEMPLATE directory contains starter templates for creating new SCSS modules consistently. This helps maintain coding standards and speeds up development.

Example of `__MODULE-TEMPLATE__.scss`:
```scss
//*** [FOLDER]: <MODULE NAME> ***//
//* Description of the module's purpose

@use '../abstracts/variables' as var;
@use '../abstracts/functions' as fn;
@use '../abstracts/mixins' as mx;

// Module Name
$_module-name: 'Module';

/* ### #{$_module-name} START */

// Local Module variables
$_module-specific-variable: value;

// Module styles
.module-name {
  // Properties
}

/* ### #{$_module-name} END
/* ------------------------------------------------------------ */
```

### Abstracts
The abstracts folder contains the project's Sass helpers: functions, mixins, and variables. These files form the foundation of your styles and should be highly reusable.

Each subfolder within abstracts follows a specific naming convention:
- Functions: `_fn-[name].scss`
- Mixins: `_mx-[name].scss`
- Variables: `_var-[name].scss`

### Vendors
The utilities folder contains helper classes and foundational styles:

- `_math-viewport.scss`: Mathematical constants and viewport-related utilities
    ```scss
    :root {
    //* Mathematical constants
    --pi: 3.1415926536;                         // The number π
    --phi: #{math.div(1 + sqrt(5), 2)};         // Golden Ratio phi φ
    --sqrt-2: #{sqrt(2)};                       // Square root of 2

    //* Viewport variables
    --vwx: 1vw;                                 // Responsive viewport unit

    // Ultra wide screens adjustment
    @include mx.mq-ultra-wide {
        --vwx: 2vh;
    }
    }
    ```
- `_a11y-helpers.scss`: Accessibility helper classes
    ```scss
    .visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
    }
    ```
- `_spacing.scss`: Spacing custom properties and utilities
- `_grid.scss`: Grid system utilities

### Themes
The themes folder contains files that define the visual aspects of your site:
- `_font-faces.scss`: Custom font declarations
- `_colors.scss`: Color custom properties and themes
- `_typography.scss`: Typography-related custom properties

Example of theme organization:*
```scss
// _colors.scss
:root {
  --color-primary: hsl(215, 100%, 50%);
  --color-primary-light: hsl(215, 100%, 65%);
  --color-primary-dark: hsl(215, 100%, 35%);
}

// _typography.scss
:root {
  --font-family-base: 'Inter', system-ui, sans-serif;
  --font-size-base: 1rem;
  --line-height-base: 1.5;
}
```

### Base
Contains styles for bare HTML elements. These styles define the default look of elements without classes.

Example structure:
```scss
// _html.scss
html {
  scroll-behavior: smooth;
  text-size-adjust: 100%;
}

// _form.scss
input,
textarea,
select {
  font: inherit;
  color: inherit;
}
```

### Components
Contains styles for specific UI components. Each component should be self-contained and reusable.

Example component structure:
```scss
// _button.scss
.button {
  // Base button styles
  &--primary {
    // Primary button variant
  }
  &--secondary {
    // Secondary button variant
  }
}
```

### Layout
Contains styles for major layout components:
- `_container.scss`: Layout wrapper styles
- `_header.scss`: Site header styles
- `_footer.scss`: Site footer styles

Example layout component:
```scss
// _container.scss
.container {
  position: relative;
  width: 100%;

  &--full-width {
    @extend .container;
    margin-inline: calc(-50% + 50vw);
  }

  &--boxed, &--narrow {
    @extend .container;
    margin-inline: auto;
    padding-inline: min(3.125%, .75rem);
    
  }

  &--boxed {
    max-width: var.$max-content-width;
  }

  &--narrow {
    max-width: calc(var.$max-content-width * .8);
  }
}
```
### Pages
Contains page-specific styles that don't fit into components or layout categories.

## File Organization Best Practices
### Index Files
Each folder should contain an _index.scss file that forwards all partials:
```scss
// utilities/_index.scss
@forward 'reset';
@forward 'math-viewport';
@forward 'a11y-helpers';
@forward 'spacing';
@forward 'grid';
```

### Main Entry File
The `style.scss` file serves as the main entry point:
```scss
// style.scss
@charset 'utf-8';

@forward './vendors';
@forward './utilities';
@forward './theme';
@forward './base';
@forward './components';
@forward './layouts';
@forward './pages';
```

### Naming Conventions
- Partial files begin with an underscore: `_filename.scss`
- Use kebab-case for file and folder names
- Use descriptive prefixes for abstract files:
    - Functions: `_fn-`
    - Mixins: `_mx-`
    - Variables: `_var-`

### Import Aliases
Use consistent aliases when importing abstract files:
```scss
@use '../abstracts/variables' as var;
@use '../abstracts/functions' as fn;
@use '../abstracts/mixins' as mx;
```

This structure promotes maintainability, scalability, and clear organization of styles while following modern SCSS best practices.


## Design system
- [Design System Overview Documentation](doc/design-system.md)<br>
A comprehensive overview of our design system principles and implementation

### Core Systems
- [Fluid Font Size Detailed Documentation](doc/fluid-font-size.md)<br>
Typography system that smoothly scales text across different viewport sizes
- [Fluid Spacing Detailed Documentation](doc/fluid-spacing.md)<br>
8-point grid system with fluid spacing that maintains proportions at any screen size
- [Media Query Mixins](doc/media-query-mixins.md)<br>
Flexible breakpoint system for consistent responsive behavior across components

