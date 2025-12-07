# Practical Activity: Sass and Modular CSS

Welcome to the **Sass** activity in GitHub Classroom. In this practice, you will work with CSS preprocessors (Sass/SCSS) to organize and modularize styles, leveraging **variables**, **mixins**, **functions**, **partials**, and **imports**.

---

## Learning Objectives

- Understand what Sass is and the **SCSS** syntax.
- Structure styles in a **modular** way with **partials** (`_*.scss`).
- Reuse code with **variables**, **mixins**, and **functions**.
- Use **nesting**, **placeholders** (`%selector`), and **@extend** responsibly.
- Configure a **build workflow** (Sass CLI or `npm` script).
- Produce clean, maintainable, and minified CSS.

---

## Project Structure

Recommended folder structure:

```
.
├── src/
│   ├── scss/
│   │   ├── _variables.scss
│   │   ├── _mixins.scss
│   │   ├── _functions.scss
│   │   ├── _base.scss         # resets, typography, base elements
│   │   ├── _layout.scss       # grid, containers, header, footer
│   │   ├── _components.scss   # buttons, cards, forms, etc.
│   │   ├── _utilities.scss    # helpers (e.g., .u-hidden, .u-visually-hidden)
│   │   └── main.scss          # entry point (imports the rest)
│   ├── index.html
│   └── assets/
│       └── images/
├── dist/
│   └── css/
│       ├── main.css
│       └── main.min.css
├── .gitignore
├── package.json (optional)
└── README.md
```

---

## Prerequisites

- Basic knowledge of **HTML** and **CSS**.
- Node.js installed (optional if using `npm scripts`).
- Sass installed (via `npm` or binary):

```bash
# Global installation (optional)
npm install -g sass

# Or as a project dependency
npm install --save-dev sass
```

---

## Configuration and Compilation

### Option A: Direct CLI

```bash
sass src/scss/main.scss dist/css/main.css --style=expanded --source-map
sass src/scss/main.scss dist/css/main.min.css --style=compressed --no-source-map
```

### Option B: `npm scripts`

Add to `package.json`:

```json
{
  "scripts": {
    "sass": "sass src/scss/main.scss dist/css/main.css --style=expanded --source-map",
    "sass:watch": "sass --watch src/scss/main.scss:dist/css/main.css --style=expanded",
    "sass:prod": "sass src/scss/main.scss dist/css/main.min.css --style=compressed --no-source-map"
  }
}
```

Run:

```bash
npm run sass        # development build
npm run sass:watch  # recompile on changes
npm run sass:prod   # production build minified
```

---

## 📋 Mandatory Tasks

### 1. Modular SCSS Structure

- Create the partials described in the structure (`_variables.scss`, `_mixins.scss`, `_functions.scss`, `_base.scss`, `_layout.scss`, `_components.scss`, `_utilities.scss`).
- Import them from `main.scss` as the single entry point.
- Maintain a clear separation between **base**, **layout**, **components**, and **utilities**.

### 2. Variables and Design Tokens

- Define color palette, typography, spacing, and breakpoints in `_variables.scss`.
- Example:

```scss
$color-primary: #4f46e5;
$color-secondary: #06b6d4;
$spacing-2: 0.5rem; // 8px
$spacing-4: 1rem;   // 16px
$bp-md: 48rem;      // 768px
```

### 3. Reusable Mixins and Functions

- Implement at least **2 mixins** (e.g., `mq()` for media queries, `btn()` for buttons, `flex-center()`).
- Implement at least **1 Sass function** (e.g., `rem($px)` to convert pixels to `rem`).
- Document them to clarify parameters and usage.

### 4. Reusable Components

- Create at least **3 components** (button, card, alert) with variants.
- Use **moderate nesting** (<3 levels) and **@extend** with **placeholders** (`%btn-base`).
- Avoid code repetition.

### 5. Responsive Design

- Apply breakpoints with mixins (e.g., `@include mq($bp-md) { ... }`).
- Ensure components are **responsive** across multiple screen sizes.
- Example: flexible layouts and organized media queries.

### 6. Accessibility

- Add utilities like `.u-visually-hidden` for accessible content.
- Include `:focus` and `:focus-visible` on interactive components (buttons, links).
- Ensure adequate color contrast.

### 7. Production Build

- Configure `npm` scripts to compile Sass to CSS.
- Generate `dist/css/main.css` (expanded + source map) and `dist/css/main.min.css` (compressed).
- Verify that the files are generated correctly.

### 8. Demonstration and Documentation

- Create `src/index.html` showing all components and variants.
- Complete the project's `README.md` with:
  - Brief explanation of partials organization and rationale.
  - List of created mixins/functions with usage examples.
  - How to run `npm run sass`, `npm run sass:watch`, etc.

---

## ⭐ Optional Part - Documentation with **mdBook**

If you want to create interactive documentation about Sass architecture, components, and best practices:

### Quick Steps

1. **Install mdBook**:

   ```bash
   cargo install mdbook
   # Or download from https://github.com/rust-lang/mdBook/releases
   ```

2. **Prepared mdBook structure**:
   - The `docs/` folder contains `book.toml` and `src/` with Markdown files.
   - Modify `src/SUMMARY.md` to organize chapters (e.g., architecture, components, build guide).

3. **Preview locally**:

   ```bash
   cd docs
   mdbook serve -p 3000
   # Open http://localhost:3000
   ```

4. **Build for production**:

   ```bash
   mdbook build
   # Generates `docs/book/` with HTML
   ```

5. **Publish to GitHub Pages**:
   - You already have a GitHub Action configured (`.github/workflows/mdbook-gh-pages.yml`).
   - Just `git push` and it will build and publish automatically to the `gh-pages` branch.
   - Configure your repo's GitHub Pages to serve from `gh-pages`.

---

## 📦 Mandatory Deliverables

- **Modular SCSS structure**: `src/scss/` folder with properly organized partials.
- **Compiled CSS files**: `dist/css/main.css` and `dist/css/main.min.css`.
- **Demonstration**: `src/index.html` showing all components.
- **Documentation in `README.md`**:
  - Brief explanation of SCSS architecture (why each partial).
  - List of implemented mixins/functions with usage examples.
  - Build instructions: how to run npm scripts.
  - (Optional) Design decisions and naming conventions (BEM, etc.).

**Optional Deliverables** (for extra credit):

- Complete documentation with **mdBook** published on GitHub Pages.
- Sass tests or advanced CSS validation.
- Design refinements or additional components.

---

## 🎯 Evaluation Criteria (Rubric)

| Criterion | Weight | Description |
| --- | --- | --- |
| **Structure and Modularity** | 25% | Correct use of partials, imports, and separation of concerns. |
| **Reusability (Variables, Mixins, Functions)** | 25% | Implementation of mixins and functions, placeholder usage, strategic variables. |
| **Generated CSS Quality** | 20% | Clarity, consistency, naming conventions (BEM or similar), moderate nesting, no duplicates. |
| **Responsiveness and Accessibility** | 15% | Well-applied breakpoints, accessibility utilities, focus styles, color contrast. |
| **Build and Documentation** | 10% | Functional npm scripts, minification, clear README explanations. |
| **Bonus: mdBook** | +5% | Interactive documentation published on GitHub Pages. |

---

## ⏰ Deadline and Submission Instructions

- **Deadline**: 19/12/2025 - 23:55
- **Submission**: Push to your Classroom-generated repository before the deadline.
- **Guidelines**:
  - Follow a style guide (BEM or similar).
  - Avoid unnecessary CSS and duplicates.
  - Include explanatory comments in complex partials.

---

## 💡 Best Practices and Tips

- **Avoid deep nesting**: More than 3 levels makes code hard to maintain.
- **Prefer mixins**: For repeated patterns; use `@extend` with **placeholders** (`%`) to avoid CSS bloat.
- **Centralize values**: Colors, spacing, breakpoints should be variables.
- **Review generated CSS**: Check file size, duplicates, and specificity.
- **Clear naming**: Use BEM (`.btn__text--primary`) or similar; avoid generic names.
- **Source maps**: Facilitate debugging during development.

---

## Quick Example (SCSS)

```scss
// _variables.scss
$color-primary: #4f46e5;
$color-secondary: #06b6d4;
$spacing-4: 1rem;
$bp-md: 48rem;

// _mixins.scss
@mixin mq($width) {
  @media (min-width: $width) {
    @content;
  }
}

@mixin btn($bg, $color: #fff) {
  background: $bg;
  color: $color;
  padding: $spacing-4 $spacing-4 * 1.5;
  border-radius: 0.5rem;
  border: 0;
  cursor: pointer;
  transition: background 0.2s ease;
  
  &:hover {
    filter: brightness(1.05);
  }
}

// _components.scss
%btn-base {
  font-weight: 600;
  line-height: 1;
}

.button {
  @extend %btn-base;
  @include btn($color-primary);
}

.button--secondary {
  @extend %btn-base;
  @include btn($color-secondary);
}

.card {
  padding: $spacing-4 * 2;
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: 0.75rem;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.04);

  @include mq($bp-md) {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: $spacing-4;
  }
}
```

---

## 📚 Resources (Optional)

- [Sass Official Documentation](https://sass-lang.com/documentation)
- [CSS Style Guides: BEM, ITCSS, SMACSS](https://getbem.com/)
- [Web Accessibility: WAI-ARIA, WCAG](https://www.w3.org/WAI/)
- [mdBook Documentation](https://rust-lang.github.io/mdBook/)

---

## 🆘 Support

If you have questions, open an **Issue** on the repository with a clear description of the problem and screenshots/reproductions.

**Happy coding! 🚀**
