
# Build i Deploy

## Build CSS amb Sass
```bash
sass src/scss/main.scss dist/css/main.css --style=expanded --source-map
sass src/scss/main.scss dist/css/main.min.css --style=compressed --no-source-map
```

## mdBook
Construcció i servidor local:
```bash
mdbook build docs
mdbook serve docs
```

## Publicació a GitHub Pages (workflow)
Crea `.github/workflows/mdbook.yml` al repo amb:
```yaml
name: Deploy mdBook
on:
  push:
    branches: [ main ]
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: dtolnay/rust-toolchain@stable
      - name: Install mdBook
        run: cargo install mdbook
      - name: Build
        run: mdbook build docs
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: docs/book
```

Activa **GitHub Pages** al repositori i selecciona *Deploy from GitHub Actions*.
