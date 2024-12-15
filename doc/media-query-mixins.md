# SCSS Media Queries Mixins

A comprehensive SCSS mixin library for handling responsive design with advanced breakpoint and orientation support. This library provides a flexible and maintainable approach to implementing media queries in your SCSS projects.

## Features

- Flexible breakpoint system with support for various viewport sizes
- Directional modifiers (-up, -down, -only) for precise control
- Optional device orientation support (portrait/landscape)
- Ultra-wide viewport handling with customizable aspect ratios
- Robust error checking and validation
- Clear and consistent syntax

## Installation

Include the mixins in your SCSS project by importing the file:

```scss
@use 'path/to/media-queries' as mq;
```

Make sure you have the required dependencies:
- `variables` module (for breakpoint definitions)
- `functions` module (for utility functions)

## Core Concepts

### Breakpoint Structure

The library uses a map of breakpoints defined in your variables file. Each breakpoint represents a minimum viewport width. For example:

```scss
$breakpoints: (
  'mobile': 320px,
  'tablet': 768px,
  'desktop': 1024px,
  'wide': 1440px
);
```

### Directional Modifiers

The system supports four types of breakpoint modifiers:

- No modifier (defaults to `-up` behavior)
- `-up`: Targets the specified breakpoint and larger viewports
- `-down`: Targets the specified breakpoint and smaller viewports
- `-only`: Targets only the specified breakpoint range

## Usage Examples

### Basic Usage

```scss
@include mq.for-breakpoint('tablet-up') {
  .container {
    max-width: 80%;
  }
}

@include mq.for-breakpoint('mobile-only') {
  .nav {
    display: none;
  }
}
```

### With Orientation

```scss
@include mq.for-breakpoint('mobile', 'portrait') {
  .sidebar {
    width: 100%;
  }
}
```

### Ultra-wide Screens

```scss
@include mq.for-ultra-wide {
  .hero {
    padding: 4rem;
  }
}

// Custom ultra-wide parameters
@include mq.for-ultra-wide('21/9', 60rem) {
  .content {
    width: 60vw;
  }
}
```

## API Reference

### for-breakpoint

```scss
@include for-breakpoint($breakpoint: 'mobile', $orientation: null)
```

Parameters:
- `$breakpoint` (String): The breakpoint to target (default: 'mobile')
  - Supports suffixes: `-up`, `-down`, `-only`
- `$orientation` (String, optional): Device orientation ('portrait' or 'landscape')

### for-ultra-wide

```scss
@include for-ultra-wide($ratio: '2/1', $min-height: 67.5rem)
```

Parameters:
- `$ratio` (String): Minimum aspect ratio (width/height)
- `$min-height` (Number): Minimum viewport height in rems

## Error Handling

The library includes comprehensive error checking for:
- Invalid breakpoint names
- Invalid breakpoint suffixes
- Invalid orientation values

Example error messages:
```
Unknown breakpoint: 'unknown'. Valid breakpoints are: mobile, tablet, desktop, wide
Invalid breakpoint suffix in 'tablet-invalid'. Valid suffixes are: -up, -down, -only
Invalid orientation: 'diagonal'. Must be one of: portrait, landscape
```

## Best Practices

1. **Consistent Breakpoints**: Define your breakpoints in a single variables file and reuse them throughout your project.

2. **Mobile-First Approach**: Start with mobile styles and use `-up` modifiers to progressively enhance for larger screens.

3. **Semantic Breakpoints**: Use meaningful names for breakpoints instead of specific pixel values in your component code.

4. **Avoid Orientation Lock**: Only use orientation queries when absolutely necessary for the user experience.

5. **Performance**: Combine media queries where possible to reduce CSS output size.