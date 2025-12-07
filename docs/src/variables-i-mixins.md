
# Variables, Mixins i Funcions

## Variables (design tokens)
```scss
// _variables.scss
$color-primary: #4f46e5;
$color-secondary: #06b6d4;
$color-neutral-700: #374151;
$spacing-2: 0.5rem; // 8px
$spacing-4: 1rem;   // 16px
$bp-md: 48rem;      // 768px
```

## Mixins
```scss
// _mixins.scss
@mixin mq($min) {
  @media (min-width: $min) { @content; }
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
```

## Funcions
```scss
// _functions.scss
@function rem($px) { @return ($px / 16) * 1rem; }
```

## Ús en components
```scss
.button { @include btn($color-primary); }
.button--secondary { @include btn($color-secondary); }
```
