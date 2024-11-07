# SCSS Boilerplate

## SASS 7-1 Folder Structure
This document explains the SASS 7-1 folder structure, organized for modularity, scalability, and maintainability. Each folder serves a specific purpose, helping to separate concerns and speed up development.

### Directory Structure example:
```plaintext
// Example Structure
//  scss/
//  |
//  |- __TEMPLATE__/
//  |    |- __MODULE-TEMPLATE__.scss
//  |
//  |- abstracts/
//  |    |- functions/
//  |    |   |- _fn-px2rem.scss
//  |    |   |- _fn-hex2rgb.scss
//  |    |   ...
//  |    |   |- _index.scss
//  |    |
//  |    |- mixins/
//  |    |   |- _mx-media-queries.scss
//  |    |   |- _mx-set-colors.scss
//  |    |   ...
//  |    |   |- _index.scss
//  |    |
//  |    |- variables/
//  |        |- _var-colors.scss
//  |        |- _var-typography.scss
//  |        |- _var-breakpoints.scss
//  |        ...
//  |        |- _index.scss
//  |
//  |- vendors/
//  |    |- _bootstrap.scss
//  |    |- _modern-reset.scss
//  |    ...
//  |    |- _index.scss
//  |
//  |- utilities/
//  |    |- _reset.scss
//  |    |- _root.scss
//  |    |- _spacing.scss
//  |    |- _grid.scss
//  |    ...
//  |    |- _index.scss
//  |
//  |- themes/
//  |    |- _font.scss
//  |    |- _colors.scss
//  |    |- _typography.scss
//  |    ...
//  |    |- _index.scss
//  |
//  |- base/
//  |    |- _html.scss
//  |    |- _body.scss
//  |    ...
//  |    |- _index.scss
//  |
//  |- components/
//  |    |- _buttons.scss
//  |    |- _carousel.scss
//  |    |- _dropdown.scss
//  |    ...
//  |    |- _index.scss
//  |
//  |- layout/
//  |    |- _header.scss
//  |    |- _sidebar.scss
//  |    |- _main.scss
//  |    |- _footer.scss
//  |    ...
//  |    |- _index.scss
//  |
//  |- pages/
//  |    |- _home.scss
//  |    |- _about.scss
//  |    ...
//  |    |- _index.scss
//  |
//  |- style.scss
```

### Folder Explanations
1. **TEMPLATE**
    - `__MODULE-TEMPLATE__.scss`: A starter template for creating new SASS partials quickly. This template includes necessary imports, naming conventions, and structure.

2. **Abstracts**
The `abstracts` folder contains foundational tools like variables, functions, and mixins, ensuring they are reusable throughout the project.
    - **Functions**: Located in abstracts/functions/, these files contain reusable SASS functions.
    Example Template: `_fn-[NAME].scss`
        ```plaintext
        //*** Abstracts Function: Name ***//
        @use '../variables' as var;
        
        @function my-function($myVar: "Default Value") {
        // Do something...
        @return $result;
        }
        ```
    - **Mixins**: Located in abstracts/mixins/, these files contain mixins for common patterns.
    Example Template: `_mx-[NAME].scss`
        ```
        //*** Abstracts Mixin: Name ***//
        @use '../variables' as var;
        @use '../functions' as fn;
        
        @mixin mixin-name($myVar: "Default Value") {
          @content;
        }
        ```
    - **Variables**: Located in abstracts/variables/, this is where global variables (e.g., colors, font sizes, and breakpoints) are defined.
    - Example Template: `_var-[NAME].scss`
        ```
        //*** Abstracts Variables: [NAME] ***//
        
        // Example variable
        $base-font-size: 16px;
        
        // Example map
        $breakpoints: (
          "mobile": 320px,
          "phablet": 540px,
          "tablet": 720px,
          "laptop": 1024px,
          "desktop": 1440px
        );
        ```

3. **Vendors**
Third-party libraries and resets, such as Bootstrap and Normalize.css, that are imported into the project.

4. **Utilites**
Contains utility classes and foundational styles like resets, root variables, spacing, and grid systems.
    - `_reset.scss`: Resets to ensure consistent styling across browsers.
    - `_root.scss`: Global variables and custom properties.
    - `_spacing.scss` and `_grid.scss`: Utility classes for spacing and grid layout.

5. **Theme**
Holds theme-specific styles like colors, fonts, and typography settings, allowing for easy customization and theming.
    - `_font.scss`: Contains @font-face rules for self-hosted fonts.
    - `_colors.scss`: Theme-specific color settings.
    - `_typography.scss`: Typography styles using global variables and theme-specific settings.

6. **Base**
Base styles for general HTML elements and structural styling that applies globally.
    - `_general.scss`: Contains global styling for elements like `html` and `body`.

7. **Components**
The `components` folder contains individual components, like buttons, carousels, and dropdowns. Each component is meant to be modular and independent.

8. **Layout**
The `layout` folder is where styles for the main page structure reside, like headers, footers, and sidebars.

9. **Pages**
The `pages` folder contains page-specific styles, such as styles that only apply to the About or Contact page.

### `_index.scss` Files
Each folder (like `abstracts/functions`, `base`, `components`, etc.) contains an `_index.scss file`. This file serves as a central point to import and consolidate all partials within that folder, making it easy to manage imports in the main `style.scss` file.

**Purpose** of `_index.scss`
- **Centralized Imports**: The `_index.scss` file imports all individual partials within its folder. For example, `abstracts/[subfolder]/_index.scss` imports all variables, functions, and mixins within each subfolder folder.
- **Organized Main Import**: Rather than listing each partial in `style.scss`, you simply import each folder’s `_index.scss`. This keeps the main file cleaner and easier to read.

### Why Use `@use` with Aliases (as `var`, as `fn`, as `mx`)
1. **Namespace Management**: Using `@use` with aliases (e.g., `var`, `fn`, `mx`) keeps your code organized and avoids naming conflicts. For instance, multiple files can define a `$primary-color` variable without conflict.
    ```
    // Example usage
    color: var.$primary-color;
    ```
2. **Improved Readability**: Descriptive aliases like var, fn, and mx make your SASS easier to read, especially in larger projects.
3. **Scoped Imports for Better Maintenance**: Using `@use` with aliases limits each import to its defined namespace, making refactoring easier.
4. **Consistent Naming**: Consistent naming conventions allow developers to immediately understand the purpose of imported items, reducing errors in large codebases.

### Example of Aliased Imports
```
@use '../abstracts/variables' as var; // All variables are scoped under 'var'
@use '../abstracts/functions' as fn;  // All functions are scoped under 'fn'
@use '../abstracts/mixins' as mx;     // All mixins are scoped under 'mx'

// Usage in a partial
.example {
  color: var.$primary-color;
  padding: fn.spacing(2);
  @include mx.flex-center;
}
```
By adopting @use with aliases, you maintain a structured, organized, and scalable SASS architecture that’s easy to read, avoids conflicts, and keeps your code maintainable.

### Main Entry File
  - `style.scss`: The main entry point that collects all other partials and builds the final compiled CSS.
