# Sass + Tailwind (Advanced/Optional)

> **Note**: This is an advanced optional topic. The base project uses **Sass only** (see `npm run build`). This section is for students who want to integrate Tailwind CSS with their Sass workflow.

## Estratègia recomanada (avançada)

- El projecte base utilitza **Sass només** per compilar a CSS.
- Si vols afegir Tailwind, pots integrar-lo mitjançant PostCSS (veure instruccions més avall).
- Això és opcional i adreçat a estudiants que volen experimentar amb utilitats CSS.

## Instal·lació (npm) — opcional

> Nota: Tailwind no ve preinstal·lat. Només instal·la si vols experimentar amb aquesta integració.

## Fitxers clau

- `tailwind.config.js` – configuració de Tailwind (theme, plugins, content).
- `postcss.config.js` – config per usar `tailwindcss` i `autoprefixer`.
- `src/scss/main.scss` – el teu Sass modular (partials, components, etc.).
- `src/styles/tailwind-input.css` – arxiu d'entrada per Tailwind amb directius `@tailwind` i import del CSS compilat per Sass.

## Exemple de `postcss.config.js`

```js
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer'),
  ]
}
```

## Pipeline i scripts (exemple)

1. Compilar Sass a un fitxer temporal (o a `dist/`):

```bash
sass src/scss/main.scss .tmp/sass.css --no-source-map
```

1. Crear un fitxer d'entrada per Tailwind (`src/styles/tailwind-input.css`) que importi el CSS generat per Sass i afegeixi les directrius de Tailwind:

```css
@import "../../.tmp/sass.css"; /* el CSS generat per Sass */

@tailwind base;
@tailwind components;
@tailwind utilities;

/* Aquí pots utilitzar @apply dins de classes si vols */
.btn-custom {
  @apply px-4 py-2 rounded bg-blue-600 text-white;
}
```

1. Processar amb PostCSS (Tailwind) i generar el CSS final:

```bash
postcss src/styles/tailwind-input.css -o dist/css/main.css
```

### Exemple de `package.json` scripts

```json
{
  "scripts": {
    "build:sass": "sass src/scss/main.scss .tmp/sass.css --no-source-map",
    "build:tailwind": "postcss src/styles/tailwind-input.css -o dist/css/main.css",
    "build": "npm run build:sass && npm run build:tailwind"
  }
}
```

Amb aquest `build` primer compiles Sass i després PostCSS/Tailwind processa la sortida.

## Notes i consells

- Si prefereixes una pipeline única (per exemple amb Vite, Webpack o Parcel), integra Sass com a loader i afegeix PostCSS amb Tailwind en la configuració; això simplifica el desenvolupament amb live-reload.
- Quan uses `@apply` dins de `.scss`, recorda que ha de processar-se després de Sass (per això treballem amb l'ordre Sass -> PostCSS).
- Mantingues el CSS generat per Sass com a base per a components personalitzats i utilitza Tailwind per a utilitats i layout ràpid.

## Resum

1. Escriu SCSS modular com sempre.
2. Compila SCSS a CSS.
3. Processa aquest CSS amb PostCSS + Tailwind.
4. Serveix o publica `dist/css/main.css`.

Aquest enfocament et dona el millor de dos mons: l'organització i abstracció de Sass i la productivitat i utilitats de Tailwind.
