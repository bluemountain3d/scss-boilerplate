# Comprehensive SCSS Design System Documentation

A complete guide to implementing a modular, scalable SCSS architecture with fluid typography, spacing, and responsive design systems.

## Table of Contents

1. [Introduction](#introduction)
2. [Project Structure](#project-structure)
3. [Core Systems](#core-systems)
   - [Fluid Typography System](#fluid-typography-system)
   - [Fluid Spacing System](#fluid-spacing-system)
   - [Media Query System](#media-query-system)
4. [Configuration](#configuration)
5. [Implementation Guide](#implementation-guide)
6. [Advanced Features](#advanced-features)
7. [Best Practices](#best-practices)
8. [Troubleshooting](#troubleshooting)

## Introduction

This documentation describes a comprehensive SCSS framework that combines three essential systems:
- A fluid typography system that creates harmonious text scaling
- A fluid spacing system based on an 8-point grid
- A flexible media query system for responsive design

These systems work together to create a cohesive design framework that maintains proper proportions across all viewport sizes while remaining maintainable and scalable.

## Project Structure

The framework follows the SASS 7-1 pattern, organized for maximum modularity and maintainability:

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
├── utilities/                   # Utility classes
├── themes/                      # Theme-specific styles
├── base/                        # Base element styles
├── components/                  # UI components
├── layout/                      # Layout components
├── pages/                       # Page-specific styles
└── style.scss                   # Main entry point
```

### Key Configuration Files

The system relies on several core configuration files:


```scss
// Base configuration for fluid systems
$size-base: (
  "min-size": 16,
  "max-size": 20,
  "min-width": 384,
  "max-width": 1920,
  "min-scale": 1.25,
  "max-scale": 1.333,
  "decimals": 4
);

// Breakpoints for media queries
$breakpoints: (
  'mobile': 320px,
  'tablet': 720px,
  'laptop': 1350px,
  'desktop': 1800px
);
```

## Core Systems

### Fluid Typography System

The typography system creates harmonious relationships between different text sizes using modular scales that adapt to viewport width.

#### Typography Scale

```scss
$font-sizes: (
  100: -2,      // Two steps smaller than base
  200: -1,      // One step smaller than base
  300: 0,       // Base size
  400: 1,       // One step larger
  // ... up to
  900: 6        // Six steps larger
);
```

Implementation:

```scss
:root {
  @include mx.fluid-font-size-var(
    $prefix: 'fs',
    $method: 'clamp'
  );
}

// Usage
.heading {
  font-size: var(--fs-400);
}
```

### Fluid Spacing System

Built on an 8-pixel baseline, the spacing system provides consistent increments that work harmoniously with the 8-point grid.

#### Spacing Scale

```scss
$spacing-weights: (
  '025': .25,   // 2px
  '050': .5,    // 4px
  '075': .75,   // 6px
  '100': 1,     // 8px (baseline)
  '150': 1.5,   // 12px
  // ... up to
  '1000': 10    // 80px
);
```

Implementation:

```scss
:root {
  @include mx.fluid-spacing-var(
    $prefix: 'gap',
    $method: 'clamp'
  );
}

// Usage
.card {
  padding: var(--gap-100);
  margin-bottom: var(--gap-200);
}
```

### Media Query System

A flexible system for handling responsive design with support for various viewport sizes and orientations.

#### Basic Usage Examples

```scss
.container {
  width: 100%;
  @include mq.for-breakpoint('tablet-up') {
    max-width: 80%;
  }
}

// With orientation
.sidebar {
  max-width: min(50%, 22.5rem);
  @include mq.for-breakpoint('mobile-only', 'portrait') {
    max-width: 100%;
  }
}

```

#### Ultra-wide Screen Support

```scss
:root {
  --vwx: 1vw;
  @include mq.for-ultra-wide {
    --vwx: 2vh;  // Prevents excessive scaling
  }
}
```

## Implementation Guide

### Step 1: Initial Setup

1. Set up your project structure following the SASS 7-1 pattern
2. Import the core abstract modules:

```scss
@use '../abstracts/variables' as var;
@use '../abstracts/functions' as fn;
@use '../abstracts/mixins' as mx;
```

### Step 2: Configure Base Systems

Set up your root configuration:

```scss
:root {
  // Viewport unit
  --vwx: 1vw;

  // Initialize fluid systems
  @include mx.fluid-spacing-var(
    $prefix: 'gap',
    $method: 'clamp'
  );

  @include mx.fluid-font-size-var(
    $prefix: 'fs',
    $method: 'clamp'
  );

  // Ultra-wide screen adjustment
  @include mx.for-ultra-wide {
    --vwx: 2vh;
  }
}
```

### Step 3: Implement Theme Settings

Create your theme variables:

```scss
:root {
  // Colors
  --color-primary: hsl(215, 100%, 50%);
  --color-primary-light: hsl(215, 100%, 65%);
  
  // Typography
  --font-family-base: 'Inter', system-ui, sans-serif;
  --line-height-base: 1.5;
}
```

## Advanced Features

### Custom Scale Creation

Create custom scales for specific components:

```scss
// Custom spacing scale
$custom-spacing: (
  'sm': 0.5,
  'md': 1,
  'lg': 2
);

:root {
  @include mx.fluid-spacing-var($custom-weights: $custom-spacing);
}
```

### Responsive Container Layouts

```scss
.container {
  position: relative;
  width: 100%;

  &--full-width {
    @extend .container;
    margin-inline: calc(-50% + 50vw);
  }

  &--boxed {
    margin-inline: auto;
    max-width: var.$max-content-width;
    padding-inline: min(3.125%, .75rem);
  }

  &--narrow {
    @extend .container--boxed;
    max-width: calc(var.$max-content-width * .8);
  }
}
```

## Best Practices

1. Typography
   - Use the base size (300) as your primary body text size
   - Maintain a consistent type hierarchy
   - Limit the number of different sizes used
   - Test readability across viewport sizes

2. Spacing
   - Use the baseline (8px) as your fundamental unit
   - Leverage quarter-step increments for fine adjustments
   - Use larger increments for major layout spacing
   - Keep consistent spacing patterns within components

3. Media Queries
   - Follow a mobile-first approach
   - Use semantic breakpoint names
   - Combine media queries where possible
   - Only use orientation queries when necessary

4. General
   - Follow the established naming conventions
   - Use index files to maintain organization
   - Keep components self-contained
   - Document new features and modifications

## Troubleshooting

### Common Issues

1. Text Scaling Issues
   - Verify scale ratio settings
   - Check viewport configuration
   - Ensure proper unit stripping

2. Spacing Inconsistencies
   - Confirm baseline settings
   - Verify weight configurations
   - Check custom property generation

3. Media Query Problems
   - Validate breakpoint names
   - Check suffix usage (-up, -down, -only)
   - Verify orientation values

### Performance Optimization

1. Custom Properties
   - Use for repeated values
   - Limit the number of generated sizes
   - Combine related properties

2. Media Queries
   - Combine where possible
   - Use breakpoint mixins consistently
   - Avoid redundant queries

For additional assistance or to report issues, please open an issue in the repository.

## Contributing

When contributing to this library:
1. Follow the established naming conventions
2. Add comprehensive documentation for new features
3. Include error handling for edge cases
4. Add examples for new functionality
5. Test across different viewport sizes

## License

This library is available under the MIT License. See the LICENSE file for more details.