# Fluid Spacing System Documentation

A comprehensive fluid spacing system that creates consistent, responsive spacing across different viewport sizes. This system uses CSS custom properties and SCSS mixins to generate spacing values that scale smoothly between minimum and maximum viewport widths.

## Table of Contents

- [Core Concepts](#core-concepts)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Technical Details](#technical-details)
- [Advanced Usage](#advanced-usage)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Core Concepts

The fluid spacing system is built around several key concepts that work together to create a flexible and maintainable spacing framework:

### Base Configuration

The system uses a fundamental configuration that defines the core parameters for fluid scaling:

```scss
$size-base: (
  "min-size": 16,
  "max-size": 20,
  "min-width": 384,
  "max-width": 1920,
  "min-scale": 1.25,
  "max-scale": 1.333,
  "decimals": 4
);
```

### Baseline and Spacing Scale

The system uses an 8px (0.5rem) baseline with a comprehensive spacing scale that provides fine-grained control through a weight system:

```scss
$spacing-weights: (
  '025': .25,  // 2px
  '050': .5,   // 4px
  '075': .75,  // 6px
  '100': 1,    // 8px (baseline)
  '150': 1.5,  // 12px
  // ... continues up to
  '1000': 10   // 80px
);
```

This scale provides consistent spacing increments that work harmoniously with the 8-point grid system.

### Fluid Scaling

The system creates smooth transitions between minimum and maximum sizes using CSS clamp() or max() functions. This ensures that spacing scales appropriately across different viewport sizes while maintaining proper proportions.

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
}

@include mx.for-ultra-wide {
  --vwx: 2vh;  // Ultra-wide screen adjustment
}
```

## Configuration

### Custom Properties

Use the fluid-spacing-var mixin to generate CSS custom properties:

```scss
:root {
  @include fluid-spacing-var(
    $prefix: 'gap',
    $method: 'clamp', // or max
    $remSize: 16,
    $baseline: 8,  // 0.5rem
    $size-multiplier: 2
  );
}
```

### Utility Classes

Generate utility classes using the fluid-spacing-util mixin:

```scss
@include fluid-spacing-util(
  $prefix: 'margin',
  $property: 'margin',
  $method: 'clamp', // or max
);
```

## Usage

### Basic Usage

Use generated custom properties in your styles:

```scss
.card {
  padding: var(--gap-100);
  margin-bottom: var(--gap-200);
  gap: var(--gap-050);
}
```

Or use utility classes:

```html
<div class="margin-100">
  <div class="padding-200">Content</div>
</div>
```

### Responsive Behavior

The spacing automatically adjusts based on viewport size:

- Below minimum width (384px): Uses minimum size
- Between minimum and maximum widths: Scales fluidly
- Above maximum width (1920px): Uses maximum size

### Ultra-wide Screen Handling

The system automatically adjusts for ultra-wide screens by switching from viewport width to height-based scaling:

```scss
@include mx.for-ultra-wide {
  --vwx: 2vh;  // Prevents excessive scaling on wide screens
}
```

## Technical Details

### The Fluid Calculation Function

The system uses a calculation function that:

1. Converts all measurements to REMs
2. Calculates the slope for fluid scaling
3. Determines the intersection point
4. Generates the appropriate CSS clamp() or max() function

```scss
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
  // Function implementation details...
}
```

### Helper Functions

The system includes several helper functions:

- strip-unit(): Removes units from values for calculations
- map-filter(): Filters spacing weights for custom implementations
- calc-fluid-size(): Generates fluid sizing values

## Advanced Usage

### Custom Weight Maps

Create custom spacing scales for specific components:

```scss
$custom-weights: (
  'sm': 0.5,
  'md': 1,
  'lg': 2
);

@include fluid-spacing-var(
  $custom-weights: $custom-weights
);
```

### Filtering Weights

Generate only specific weights:

```scss
@include fluid-spacing-var(
  $include-weights: ('100', '200', '300')
);
```

### Debug Mode

Enable debug output to see calculated values:

```scss
@include fluid-spacing-var(
  $debug: true
);
```

## Best Practices

1. Use the baseline (8px) as your fundamental unit of measurement
2. Leverage the quarter-step increments for fine adjustments
3. Use larger increments for major layout spacing
4. Consider switching to height-based scaling for ultra-wide screens
5. Keep consistent spacing patterns within components
6. Use the generated custom properties instead of hard-coded values

## Troubleshooting

Common issues and solutions:

1. Unexpected Scaling
   - Verify viewport configuration
   - Check min/max width settings
   - Ensure proper unit stripping

2. Missing Values
   - Confirm weight is included in spacing map
   - Check for proper mixin inclusion
   - Verify custom weight configurations

3. Performance Issues
   - Use custom properties instead of utility classes for frequently repeated values
   - Consider reducing the number of generated weights
   - Optimize media query usage

For additional assistance or bug reports, please open an issue in the repository.