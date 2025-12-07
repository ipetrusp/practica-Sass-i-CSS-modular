
# Components

## Botons
```scss
%btn-base { font-weight: 600; line-height: 1; }
.button { @extend %btn-base; @include btn($color-primary); }
.button--secondary { @extend %btn-base; @include btn($color-secondary); }
```

## Targetes
```scss
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

## Alertes
```scss
.alert { padding: $spacing-4; border-left: 4px solid $color-secondary; background: #f0f9ff; }
```
