# Activitat pràctica: Sass i CSS modular

Benvingut/da a l'activitat de **Sass** dins de GitHub Classroom. En aquesta pràctica treballaràs amb precompiladors CSS (Sass/SCSS) per organitzar i modularitzar estils, aprofitant **variables**, **mixins**, **funcions**, **partials** i **imports**.

Pots consultar la documentació de SASS a https://ipetrusp.github.io/practica-Sass-i-CSS-modular/

---

## Objectius d'aprenentatge

- Entendre què és Sass i la sintaxi **SCSS**.
- Estructurar estils de manera **modular** amb **partials** (`_*.scss`).
- Reutilitzar codi amb **variables**, **mixins** i **funcions**.
- Utilitzar **nesting**, **placeholders** (`%selector`) i **@extend** de manera responsable.
- Configurar un **workflow** de compilació (CLI de Sass o un script de `npm`).
- Produir CSS net, mantenible i minimitzat.

---

## Estructura del projecte

Recomanació d'estructura de carpetes:

```
.
├── src/
│   ├── scss/
│   │   ├── _variables.scss
│   │   ├── _mixins.scss
│   │   ├── _functions.scss
│   │   ├── _base.scss         # resets, tipografia, elements base
│   │   ├── _layout.scss       # grid, contenidors, capçalera, peu de pàgina
│   │   ├── _components.scss   # botons, targetes, formularis, etc.
│   │   ├── _utilities.scss    # helpers (p. ex. .u-hidden, .u-visually-hidden)
│   │   └── main.scss          # punt d'entrada (importa la resta)
│   ├── index.html
│   └── assets/
│       └── images/
├── dist/
│   └── css/
│       ├── main.css
│       └── main.min.css
├── .gitignore
├── package.json (opcional)
└── README.md
```

---

## Requisits previs

- Coneixements bàsics de **HTML** i **CSS**.
- Node.js instal·lat (opcional si utilitzes `npm scripts`).
- Sass instal·lat (via `npm` o binari):

```bash
# Instal·lació global (opcional)
npm install -g sass

# O com a dependència del projecte
npm install --save-dev sass
```

---

## Configuració i compilació

### Opció A: CLI directa

```bash
sass src/scss/main.scss dist/css/main.css --style=expanded --source-map
sass src/scss/main.scss dist/css/main.min.css --style=compressed --no-source-map
```

### Opció B: `npm scripts`

Afegiu al `package.json`:

```json
{
  "scripts": {
    "sass": "sass src/scss/main.scss dist/css/main.css --style=expanded --source-map",
    "sass:watch": "sass --watch src/scss/main.scss:dist/css/main.css --style=expanded",
    "sass:prod": "sass src/scss/main.scss dist/css/main.min.css --style=compressed --no-source-map"
  }
}
```

Execució:

```bash
npm run sass        # build de desenvolupament
npm run sass:watch  # recompila en canvis
npm run sass:prod   # build de producció minimitzat
```

---

## 📋 Tasques obligatòries

### 1. Estructura SCSS modular

- Crea els partials descrits a l'estructura (`_variables.scss`, `_mixins.scss`, `_functions.scss`, `_base.scss`, `_layout.scss`, `_components.scss`, `_utilities.scss`).
- Importa'ls des de `main.scss` com a punt d'entrada únic.
- Mantén una separació clara entre **base**, **layout**, **components** i **utilities**.

### 2. Variables i design tokens

- Defineix paleta de colors, tipografies, espaiats i breakpoints a `_variables.scss`.
- Exemple:

```scss
$color-primary: #4f46e5;
$color-secondary: #06b6d4;
$spacing-2: 0.5rem; // 8px
$spacing-4: 1rem;   // 16px
$bp-md: 48rem;      // 768px
```

### 3. Mixins i funcions reutilitzables

- Implementa almenys **2 mixins** (p. ex. `mq()` per media queries, `btn()` per botó, `flex-center()`).
- Implementa almenys **1 funció Sass** (p. ex. `rem($px)` per convertir píxels a `rem`).
- Documenta'ls per clarificar paràmetres i ús.

### 4. Components reutilitzables

- Crea com a mínim **3 components** (botó, targeta, alerta) amb variants.
- Utilitza **nesting moderat** (<3 nivells) i **@extend** amb **placeholders** (`%btn-base`).
- Evita repeticions de codi.

### 5. Responsive design

- Aplica breakpoints amb mixins (p. ex. `@include mq($bp-md) { ... }`).
- Assegura que els components siguin **responsius** en múltiples mides de pantalla.
- Exemple: layouts flexibles i media queries organitzades.

### 6. Accessibilitat

- Afegeix utilitats com `.u-visually-hidden` per a contingut accessible.
- Inclou `:focus` i `:focus-visible` en components interactius (botons, links).
- Assegura contrast de colors adequat.

### 7. Build de producció

- Configura scripts `npm` per compilar Sass a CSS.
- Genera `dist/css/main.css` (expanded + source map) i `dist/css/main.min.css` (compressed).
- Verifica que els fitxers es generin correctament.

### 8. Demostració i documentació

- Crea `src/index.html` mostrant tots els components i variants.
- Completa el `README.md` del projecte amb:
  - Com s'organitzen els partials i per què (breu descripció d'estratègia).
  - Quins mixins/funcions s'han creat i exemples d'ús.
  - Com executar `npm run sass`, `npm run sass:watch`, etc.

---

## ⭐ Part opcional - Documentació amb **mdBook**

Si vols crear documentació interactiva sobre l'arquitectura Sass, components i bones pràctiques:

### Passos ràpids

1. **Instal·lar mdBook**:

   ```bash
   cargo install mdbook
   # O descarregar des de https://github.com/rust-lang/mdBook/releases
   ```

2. **Estructura mdBook ja preparada**:
   - La carpeta `docs/` conté `book.toml` i `src/` amb fitxers Markdown.
   - Modifica `src/SUMMARY.md` per organitzar capítols (p. ex. arquitectura, components, guia de build).

3. **Prévisualitza localment**:

   ```bash
   cd docs
   mdbook serve -p 3000
   # Obrir http://localhost:3000
   ```

4. **Construir per producció**:

   ```bash
   mdbook build
   # Genera `docs/book/` amb HTML
   ```

5. **Publicar a GitHub Pages**:
   - Ja tens una GitHub Action configurada (`.github/workflows/mdbook-gh-pages.yml`).
   - Només fes `git push` i es construirà i publicarà automàticament al branch `gh-pages`.
   - Configura les GitHub Pages del repo per servir des de `gh-pages`.

---

## 📦 Lliurables obligatoris

- **Estructura SCSS modular**: carpeta `src/scss/` amb partials correctament organitzats.
- **Fitxers CSS compilats**: `dist/css/main.css` i `dist/css/main.min.css`.
- **Demostració**: `src/index.html` mostrant tots els components.
- **Documentació al `README.md`**:
  - Explicació breu de l'arquitectura SCSS (per què cada partial).
  - Llistat de mixins/funcions implementats amb exemples d'ús.
  - Instruccions de build: com executar els scripts npm.
  - (Opcional) Decisions de disseny i convencions (BEM, etc.).

**Lliurables opcionals** (per a puntuació extra):

- Documentació completa amb **mdBook** publicada a GitHub Pages.
- Tests Sass o validació CSS avançada.
- Refinaments de disseny o components addicionals.

---

## 🎯 Criteris d'avaluació (rúbrica)

| Criteri | Pes | Descripció |
| --- | --- | --- |
| **Estructura i modularitat** | 25% | Ús correcte de partials, imports i separació de responsabilitats. |
| **Reutilització (Variables, Mixins, Funcions)** | 25% | Implementació de mixins i funcions, ús de placeholders, variables estratègiques. |
| **Qualitat del codi CSS generat** | 20% | Claredat, consistència, nomenclatura (BEM o similar), nesting moderat, sense duplicitats. |
| **Responsivitat i Accessibilitat** | 15% | Breakpoints ben aplicats, utilitats d'accessibilitat, focus styles, contrast de colors. |
| **Build i Documentació** | 10% | Scripts npm funcionals, minificació, explicacions clares al README. |
| **Bonus: mdBook** | +5% | Documentació interactiva publicada a GitHub Pages. |

---

## ⏰ Terminis i instruccions d'entrega

- **Data límit**: 19/12/2025 - 23:55
- **Entrega**: push al repositori de Classroom abans de l'hora límit.
- **Normes**:
  - Segueix guia d'estil (BEM o similar).
  - Evita CSS innecessari i duplicats.
  - Inclou comentaris explicatius en partials complexos.

---

## 💡 Bones pràctiques i consells

- **Evita nesting profund**: més de 3 nivells fa el codi difícil de mantenir.
- **Prefereix mixins**: per a patrons repetits; usa `@extend` amb **placeholders** (`%`) per evitar CSS inflat.
- **Centralitza valors**: colors, espaiats, breakpoints han de ser variables.
- **Revisa el CSS generat**: verifica mida, duplicitats i especificitat.
- **Nomenclatura clara**: usa BEM (`.btn__text--primary`) o similar, evita noms genèrics.
- **Source maps**: facilitate debugging durant desenvolupament.

---

## Exemple ràpid (SCSS)

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

## 📚 Recursos (opcionals)

- [Documentació oficial de Sass](https://sass-lang.com/documentation)
- [Guies d'estil CSS: BEM, ITCSS, SMACSS](https://getbem.com/)
- [Accessibilitat web: WAI-ARIA, WCAG](https://www.w3.org/WAI/)
- [mdBook Documentation](https://rust-lang.github.io/mdBook/)

---

## 🆘 Suport

Si tens dubtes, obre un **Issue** al repositori amb una descripció clara del problema i captures/reproduccions.

**Bona pràctica! 🚀**
