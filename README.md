# GurrLab Onboarding & Resources

The official onboarding guide for the [GurrLab](https://github.com/GurrLab) at Hatfield Marine Science Center, Oregon State University.

Built with [bookdown](https://bookdown.org). The live site is published via GitHub Pages.

---

## Contents

| File | Chapter |
|---|---|
| `index.Rmd` | Cover & navigation |
| `01-welcome.Rmd` | Getting started — accounts, contacts, norms |
| `02-philosophy.Rmd` | Lab philosophy — five pillars, critique culture |
| `03-conduct.Rmd` | Code of conduct & bidirectional expectations |
| `04-computing.Rmd` | Bash, Git/GitHub, R, HPC tutorials |
| `05-lab-spaces.Rmd` | Lab spaces, equipment, collaborations |
| `06-guide.Rmd` | Role-specific onboarding guide |

## Building locally

```r
install.packages("bookdown")
bookdown::render_book("index.Rmd", "bookdown::gitbook")
```

Output goes to `_book/`. Open `_book/index.html` to preview.

## Deploying to GitHub Pages

1. Push all source files to the `main` branch
2. Go to **Settings → Pages → Source: Deploy from branch → `gh-pages`** (or `main/docs` if you prefer)
3. Run `bookdown::render_book()` and push the `_book/` contents to the `gh-pages` branch, or use the GitHub Actions workflow below

### GitHub Actions (auto-deploy on push)

Create `.github/workflows/bookdown.yml`:

```yaml
on:
  push:
    branches: [main]
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: r-lib/actions/setup-r@v2
      - uses: r-lib/actions/setup-pandoc@v2
      - run: Rscript -e 'install.packages(c("bookdown","rmarkdown"))'
      - run: Rscript -e 'bookdown::render_book("index.Rmd")'
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_book
```

Your live URL will be: `https://gurrlab.github.io/Onboarding/`

## Placeholders to fill in

Search for `[` in any `.Rmd` file to find all placeholder text that needs real content:
building/room numbers, collaborator names and emails, equipment models, HPC documentation URL, vessel name, field site coordinates.

---

*Contact: [samuel.gurr@oregonstate.edu](mailto:samuel.gurr@oregonstate.edu)*
