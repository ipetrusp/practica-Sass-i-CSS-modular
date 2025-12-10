
# Sass + Bootstrap 5

Aquest apartat explica com personalitzar i estendre Bootstrap 5 utilitzant la seva versió en **Sass** (sources) per tenir un workflow modular i mantenible.

## Per què usar Sass amb Bootstrap?

- Bootstrap 5 proporciona fitxers `.scss` que permeten sobreescriure variables, mapes i mixins abans d'importar els components.
- Això facilita crear un tema consistent (colors, tipografies, espaiats) i mantenir la separació entre base i personalitzacions.

## Instal·lació (npm)

```bash
npm install bootstrap@5 sass --save-dev
```

## Estructura recomanada

```text
src/
├── scss/
|   ├── vendor/
|   |   └── _bootstrap.scss   # import del bootstrap source (o importa directament des de node_modules)
|   ├── _variables.scss       # variables i tokens del projecte (sobreescriure Bootstrap aquí)
|   ├── _bootstrap-custom.scss# imports i paràmetres de Bootstrap personalitzats
|   └── main.scss             # punt d'entrada que importa tot
```

### Exemple de personalització

1. Crea `_variables.scss` amb les teves variables (has d'establir-les abans d'importar Bootstrap):

```scss
// _variables.scss
$primary: #0d6efd; // substitueix per la teva paleta
$body-font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
$spacer: 1rem;
```

1. Importa les variables i després els fitxers de Bootstrap en un fitxer d'ajunt:

```scss
// _bootstrap-custom.scss
@import 'variables';
// Opcional: importa només parts concretes de Bootstrap per reduir mida
@import 'node_modules/bootstrap/scss/functions';
@import 'node_modules/bootstrap/scss/variables';
@import 'node_modules/bootstrap/scss/mixins';
@import 'node_modules/bootstrap/scss/root';
@import 'node_modules/bootstrap/scss/reboot';
@import 'node_modules/bootstrap/scss/type';
@import 'node_modules/bootstrap/scss/buttons';
// ...altres components que necessitis
```

1. `main.scss`:

```scss
@import 'bootstrap-custom';
@import 'components'; // els teus components personalitzats
```

### Construcció

Utilitza `sass` per compilar `src/scss/main.scss` a `dist/css` com ja està descrit al README:

```bash
npm run sass
```

### Consells

- Importa només els components de Bootstrap que utilitzis per reduir el CSS final.
- Utilitza placeholders i mixins propis per estendre estils de Bootstrap sense duplicar codi.
- Documenta quines variables de Bootstrap sobreescrius i on (afegeix comentaris a `_variables.scss`).
