
# Arquitectura SCSS

L’arquitectura es basa en **partials** i una separació per capes:

- **Base** (`_base.scss`): resets i tipografia.
- **Layout** (`_layout.scss`): contenidors, grid i regions.
- **Components** (`_components.scss`): botons, targetes, alertes.
- **Utilities** (`_utilities.scss`): classes d’ajut (p. ex. `.u-visually-hidden`).
- **Variables/Mixins/Funcions**: tokens i utilitats transversals.

## Importació a `main.scss`
```scss
@use 'variables' as *;
@use 'mixins' as mixins;
@use 'functions' as fn;
@use 'base';
@use 'layout';
@use 'components';
@use 'utilities';
```

> Pots utilitzar `@forward` per reexportar mòduls quan calgui.
