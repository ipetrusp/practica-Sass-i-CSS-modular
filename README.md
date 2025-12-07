
# Activitat pràctica: Sass i CSS modular

Benvingut/da a l’activitat de **Sass** dins de GitHub Classroom. En aquesta pràctica treballaràs amb precompiladors CSS (Sass/SCSS) per organitzar i modularitzar estils, aprofitant **variables**, **mixins**, **funcions**, **partials** i **imports**.

---

## 🎯 Objectius d’aprenentatge
- Entendre què és Sass i la sintaxi **SCSS**.
- Estructurar estils de manera **modular** amb **partials** (`_*.scss`).
- Reutilitzar codi amb **variables**, **mixins** i **funcions**.
- Utilitzar **nesting**, **placeholders** (`%selector`) i **@extend`** de manera responsable.
- Configurar un **workflow** de compilació (CLI de Sass o un script de `npm`).
- Produir CSS net, mantenible i minimitzat.

---

## 📁 Estructura del projecte
Recomanació d’estructura de carpetes:

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
│   │   └── main.scss          # punt d’entrada (importa la resta)
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

## ✅ Requisits previs
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

## ⚙️ Configuració i compilació
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

## 🧩 Tasques de l’activitat
1. **Estructura SCSS modular**
   - Crea els partials descrits a l’estructura i importa’ls des de `main.scss`.
   - Mantén una separació clara entre **base**, **layout**, **components** i **utilities**.

2. **Variables i design tokens**
   - Defineix paleta de colors, tipografies, espaiats i breakpoints a `_variables.scss`.
   - Exemple:
   ```scss
   $color-primary: #4f46e5;
   $color-secondary: #06b6d4;
   $spacing-2: 0.5rem; // 8px
   $spacing-4: 1rem;   // 16px
   $bp-md: 48rem;      // 768px
   ```

3. **Mixins i funcions**
   - Implementa almenys **dos mixins** (p. ex. per `flex-center`, `media-query`, `button-variant`).
   - Implementa **una funció** (p. ex. `rem($px)` per convertir píxels a `rem`).

4. **Components reutilitzables**
   - Crea com a mínim **tres components** (botó, targeta, alerta) amb variants.
   - Utilitza **nesting** moderat i **@extend** amb **placeholders** (`%btn-base`).

5. **Responsive design**
   - Aplica breakpoints amb mixins i assegura que els components siguin **responsius**.

6. **Accessibilitat**
   - Afegeix utilitats com `.u-visually-hidden` i focus visible.

7. **Build de producció**
   - Genera `dist/css/main.css` i `dist/css/main.min.css`.

8. **Documentació**
   - Completa aquest `README.md` amb decisions de disseny i captura d’exemples d’ús.

---

## 📌 Lliurables
- Codi al repositori amb l’estructura indicada.
- `dist/css/main.css` i `dist/css/main.min.css` generats.
- `index.html` demostrant l’ús dels components.
- Notes breus al `README` sobre:
  - Com s’organitzen els partials i per què.
  - Quins mixins/funcions s’han creat i on s’utilitzen.
  - Com s’ha configurat el procés de build.

---

## 🧪 Criteris d’avaluació (rubric)
- **Estructura i modularitat (30%)**: ús correcte de partials i imports.
- **Reutilització (25%)**: variables, mixins, funcions i placeholders.
- **Qualitat CSS (20%)**: claredat, consistència, nomenclatura (p. ex. BEM), nesting moderat.
- **Responsivitat i accessibilitat (15%)**: breakpoints, focus, utilitats.
- **Build i documentació (10%)**: scripts, minificació, explicacions al README.

---

## 🗓️ Terminis i directrius
- **Data límit**: 19/12/2025 - 23:55
- **Entrega**: push al repositori de Classroom abans de l’hora límit.
- **Normes**: segueix guia d’estil (BEM o similar) i evita CSS innecessari.

---

## 🔍 Bones pràctiques i consells
- Evita **nesting profund** (>3 nivells).
- Prefereix **mixins** per a patrons repetits; usa `@extend` amb **placeholders** per evitar CSS inflat.
- Centralitza **breakpoints** i espaiats en variables.
- Revisa el CSS generat: mida, duplicitats i especificitat.

---

## 🧠 Exemple ràpid (SCSS)
```scss
// _mixins.scss
@mixin mq($width) {
  @media (min-width: $width) { @content; }
}

@mixin btn($bg, $color: #fff) {
  background: $bg;
  color: $color;
  padding: $spacing-4 $spacing-4 * 1.5;
  border-radius: .5rem;
  border: 0;
  cursor: pointer;
  transition: background .2s ease;
  &:hover { filter: brightness(1.05); }
}

// _components.scss
%btn-base { font-weight: 600; line-height: 1; }

.button { @extend %btn-base; @include btn($color-primary); }
.button--secondary { @extend %btn-base; @include btn($color-secondary); }

.card {
  padding: $spacing-4 * 2;
  border: 1px solid rgba(0,0,0,.08);
  border-radius: .75rem;
  box-shadow: 0 4px 12px rgba(0,0,0,.04);
  @include mq($bp-md) {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: $spacing-4;
  }
}
```

---

## 🧭 Recursos (opcionals)
- Documentació oficial de Sass.
- Guies d’estil CSS (BEM, ITCSS, SMACSS).
- Accessibilitat web (WAI-ARIA, WCAG) per a utilitats i focus.

---

## 💬 Suport
Si tens dubtes, obre un **Issue** al repositori amb una descripció clara del problema i captures/reproduccions.

Bona pràctica! 🧑‍💻✨
