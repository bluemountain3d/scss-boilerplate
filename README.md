# SCSS Boilerplate

## SASS 7-1 Folder Structure
This document explains the SASS 7-1 folder structure, organized for modularity, scalability, and maintainability. Each folder serves a specific purpose, helping to separate concerns and speed up development.

### Directory Structure:
```plaintext
scss/
|
|- __TEMPLATES__
|    |- __MODULE-TEMPLATE__.scss
|
|- abstracts/
|    |- functions/
|    |   |- _fn-px2rem.scss
|    |   |- _fn-hex2rgb.scss
|    |   ...
|    |   |- _index.scss
|    |
|    |- mixins/
|    |   |- _mx-media-queries.scss
|    |   |- _mx-set-colors.scss
|    |   ...
|    |   |- _index.scss
|    |
|    |- variables/
|    |   |- _var-colors.scss
|    |   |- _var-fonts.scss
|    |   |- _var-breakpoints.scss
|    |   ...
|    |   |- _index.scss
|    |
|    ... other abstract files
|    |- _index.scss
|
|- base/
|    |- _root.scss
|    |- _reset.scss
|    |- _typography.scss
|    ...
|    |- _index.scss
|
|- utilities/
|    |- _spacing.scss
|    |- _grid.scss
|    ...
|    |- _index.scss
|
|- components/
|    |- _buttons.scss
|    |- _carousel.scss
|    |- _dropdown.scss
|    ...
|    |- _index.scss
|
|- layout/
|    |- _header.scss
|    |- _sidebar.scss
|    |- _footer.scss
|    ...
|    |- _index.scss
|
|- pages/
|    |- _about.scss
|    |- _contact.scss
|    ...
|    |- _index.scss
|
|- themes/
|    |- _theme.scss
|    |- _admin.scss
|    ...
|    |- _index.scss
|
|- vendors/
|    |- _bootstrap.scss
|    |- _modern-reset.scss
|    ...
|    |- _index.scss
|
|- style.scss
```

### Folder Explanations
1. **TEMPLATES**
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
    //*** Abstracts Variables: Name ***//
    
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
    
3. **Base**
The `base` folder contains foundational styles, like resets, typography, and root element styling.
- `_font.scss`: Sets `@font-face` rules for self hosted fonts.
- `_root.scss`: Sets custom properties or global font sizes.
- `_reset.scss`: Contains CSS resets to ensure consistent styling across browsers.
- `_typography.scss`: Defines base typography settings.

4. **Utilities**
The `utilities` folder contains helper classes, like grids, and spacing definitions.
- **Example**: `_spacing.scss` might include margin and padding utility classes.
- **Example**: `_grid.scss` contains grid system styles.

5. **Components**
The `components` folder contains individual components, like buttons, carousels, and dropdowns. Each component is meant to be modular and independent.

6. **Layout**
The `layout` folder is where styles for the main page structure reside, like headers, footers, and sidebars.

7. **Pages**
The `pages` folder contains page-specific styles, such as styles that only apply to the About or Contact page.

8. **Themes**
The `themes` folder contains theme-specific styles, making it easy to switch between different themes or adjust specific settings.

9. **Vendors**
The `vendors` folder contains third-party libraries or frameworks that need to be imported, such as Bootstrap or Normalize.css.

#### `_index.scss` Files
Each folder (like `abstracts`, `base`, `components`, etc.) contains an _index.scss file. This file serves as a central point to import and consolidate all partials within that folder, making it easy to manage imports in the main `style.scss` file.

**Purpose** of `_index.scss`
- **Centralized Imports**: The `_index.scss` file imports all individual partials within its folder. For example, `abstracts/_index.scss` imports all variables, functions, and mixins from the subfolders in the abstracts folder.
- **Organized Main Import**: Rather than listing each partial in `style.scss`, you simply import each folder’s `_index.scss`. This keeps the main file cleaner and easier to read.

### Main Entry File
- `style.scss`: The main entry point that collects all other partials and builds the final compiled CSS.