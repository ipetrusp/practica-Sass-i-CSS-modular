
# Responsive i Accessibilitat

## Breakpoints
Centralitza els breakpoints en variables i utilitza mixins `mq`.

## Accessibilitat
- Focus visible per elements interactius.
- Classe `.u-visually-hidden` per a textos de suport.

```scss
.u-visually-hidden {
  position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px;
  overflow: hidden; clip: rect(0, 0, 0, 0); border: 0;
}
```
