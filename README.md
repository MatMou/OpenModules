# Finance Course Materials

Online course materials for **Financial Econometrics**, **Statistics for Finance**, and **Valuation**, built with [Jupyter Book](https://jupyterbook.org).

## Structure

```
├── _config.yml          # Book configuration
├── _toc.yml             # Table of contents
├── intro.md             # Landing page
├── requirements.txt     # Python dependencies
├── finance/             # Financial Econometrics module
│   ├── intro.md
│   ├── returns_and_stylized_facts.ipynb
│   └── volatility_modeling.md
├── statistics/          # Statistics for Finance module
│   ├── intro.md
│   ├── distributions_and_inference.md
│   └── regression_and_diagnostics.md
└── valuation/           # Valuation module
    ├── intro.md
    ├── dcf_fundamentals.md
    └── multiples_and_comparables.md
```

## Building Locally

```bash
# Install dependencies
pip install -r requirements.txt

# Build the book
jupyter-book build .

# Open in browser
open _build/html/index.html   # macOS
# or
start _build/html/index.html  # Windows
```

## Publishing to GitHub Pages

The site is automatically built and published via GitHub Actions on every push to `main`.

**One-time setup required:**

1. Go to your repository → **Settings** → **Pages**
2. Under *Source*, select **GitHub Actions**
3. Push any change to `main` — the workflow will handle the rest

The site will be available at: `https://<your-username>.github.io/<repo-name>/`

## Adding Content

- Add `.md` files for text-heavy chapters
- Add `.ipynb` files for chapters with Python code
- Register every new file in `_toc.yml`
- Push to `main` — the site rebuilds automatically
