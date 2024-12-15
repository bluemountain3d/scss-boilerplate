# Fluid Typography and Spacing System Documentation

A comprehensive system for creating harmonious, responsive typography and spacing that adapts fluidly across different viewport sizes. This system combines modular scales for typography with an 8-point grid for spacing, creating a cohesive design framework that maintains proper proportions at any screen size.

## Table of Contents

- [System Overview](#system-overview)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Core Concepts](#core-concepts)
- [Configuration](#configuration)
- [Usage](#usage)
- [Advanced Features](#advanced-features)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## System Overview

The fluid design system consists of two main components that work together:

1. A typography system based on modular scales that creates harmonious relationships between different text sizes
2. A spacing system built on an 8-pixel baseline that provides consistent spacing increments

Both systems use CSS custom properties and fluid scaling to create smooth transitions between viewport sizes.

## Installation

1. Set up your project structure following the abstracts pattern:

```scss      
scss/abstracts/                   
  ├── functions/              // Utility functions
  │   ├── _fn-[name].scss
  │   └── _index.scss
  ├── mixins/                 // System mixins
  │   ├── _mx-[name].scss
  │   └── _index.scss
  └── variables/              // All configuration variables
       ├── _var-[name].scss
       └── _index.scss

scss/
  └── main.scss         // Your main stylesheet
```

2. Import the abstract modules in your stylesheets:

```scss
@use '../abstracts/variables' as var;
@use '../abstracts/functions' as fn;
@use '../abstracts/mixins' as mx;
```

3. Set up your viewport variables:

```scss
:root {
  --vwx: 1vw;  // Responsive viewport unit

  @include mx.for-ultra-wide {
    --vwx: 2vh;  // Ultra-wide screen adjustment
  }
}
```

## Project Structure

### Variables (_variables.scss)

Contains all configuration maps and settings:

```scss
// Base configuration
$size-base: (
  "min-size": 16,
  "max-size": 20,
  "min-width": 384,
  "max-width": 1920,
  "min-scale": 1.25,
  "max-scale": 1.333,
  "decimals": 6
);

// Spacing scale
$spacing-weights: (
  '025': .25,   // 2px
  '050': .5,    // 4px
  '100': 1,     // 8px (baseline)
  // ... up to
  '1000': 10    // 80px
);

// Typography scale
$font-sizes: (
  100: -2,      // Two steps smaller than base
  200: -1,      // One step smaller than base
  300: 0,       // Base size
  // ... up to
  900: 6        // Six steps larger than base
);
```

### Functions (_functions.scss)

Contains utility functions for calculations:

```scss
// Remove units from values
@function strip-unit($value) {
  @if type-of($value) == 'number' and not unitless($value) {
    @return math.div($value, ($value * 0 + 1));
  }
  @return $value;
}

// Filter map entries
@function map-filter($map, $keys) {
  $result: ();
  @each $key, $value in $map {
    @if index($keys, $key) {
      $result: map-merge($result, ($key: $value));
    }
  }
  @return $result;
}

// Calculate fluid sizes
@function calc-fluid-size(
  $remSize,
  $minWidth,
  $maxWidth,
  $decimals,
  $method,
  $minSize,
  $maxSize,
  $vwx: false
) {
  // Implementation details...
}
```

### Mixins (_mixins.scss)

Contains the core system mixins:

```scss
// Generate spacing custom properties
@mixin fluid-spacing-var(
  $method: 'clamp',
  $prefix: 'gap',
  // ... other parameters
) {
  // Implementation details...
}

// Generate typography custom properties
@mixin fluid-font-size-var(
  $prefix: 'fs',
  $method: 'clamp',
  // ... other parameters
) {
  // Implementation details...
}
```

## Core Concepts

### Spacing System

Built on an 8-pixel baseline, the spacing system provides consistent increments that work harmoniously with the 8-point grid. The spacing scale uses quarter-step increments for fine control at smaller sizes and larger steps for major layout elements.

### Typography System

Uses modular scales to create mathematically related text sizes. The system smoothly transitions between different scale ratios (1.25 at small screens to 1.333 at large screens) to maintain proper typographic hierarchy across all viewport sizes.

## Usage

### Basic Implementation

Initialize both systems in your root styles:

```scss
:root {
  // Initialize spacing system
  @include mx.fluid-spacing-var(
    $prefix: 'gap',
    $method: 'clamp'
  );

  // Initialize typography system
  @include mx.fluid-font-size-var(
    $prefix: 'fs',
    $method: 'clamp'
  );
}
```

### Using Custom Properties

Apply the generated properties in your styles:

```scss
.card {
  // Typography
  font-size: var(--fs-400);
  
  // Spacing
  padding: var(--gap-200);
  margin-bottom: var(--gap-300);
  gap: var(--gap-100);
}
```

[Additional sections continue as in previous README, updated with new import structure...]

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

// Custom type scale
$custom-type: (
  'small': -1,
  'base': 0,
  'large': 1
);

:root {
  @include mx.fluid-spacing-var($custom-weights: $custom-spacing);
  @include mx.fluid-font-size-var($custom-sizes: $custom-type);
}
```

[Continue with Best Practices and Troubleshooting sections as before...]

For additional assistance or to report issues, please open an issue in the repository.

## Best Practices

1. Use the base size (300) as your primary body text size
2. Maintain a consistent type hierarchy using the scale steps
3. Limit the number of different sizes used in a single design
4. Consider readability across different device sizes
5. Use the scale ratios to create harmonious relationships
6. Test typography across different viewport sizes

## Troubleshooting

Common issues and solutions:

1. Text Scaling Issues
   - Verify scale ratio settings
   - Check viewport configuration
   - Ensure proper unit stripping

2. Inconsistent Sizes
   - Confirm base size settings
   - Check scale step values
   - Verify custom property generation

3. Performance Considerations
   - Use custom properties for repeated values
   - Limit the number of generated sizes
   - Optimize media query usage

For additional assistance or to report issues, please open an issue in the repository.