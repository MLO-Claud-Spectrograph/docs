# MLO Spectrograph Software Documentation

Sphinx (RTD) documentation for spectrograph software.

The site is designed to be hosted from this repository with GitHub Pages while
using the Read the Docs Sphinx theme. It documents the cross-package user
workflow as well as the individual ETC, simulator, pipeline, shared-data, and
instrument-control repositories.

## Build locally

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
make html
```

The built site will be written to `docs/_build/html/`.

For a strict build that treats warnings as errors:

```bash
make html-strict
```

## Publish with GitHub Pages

1. Push this repository to GitHub.
2. Open **Settings -> Pages**.
3. Set **Source** to **GitHub Actions**.
4. Push to `main`, or run the `Deploy documentation` workflow manually.

The workflow in `.github/workflows/pages.yml` builds the Sphinx site and deploys
it with the official GitHub Pages actions.

## Repository layout

```text
.
├── .github/workflows/pages.yml
├── docs/
│   ├── conf.py
│   ├── index.rst
│   ├── getting-started.rst
│   ├── user-guide/
│   ├── packages/
│   ├── reference/
│   └── _static/custom.css
├── Makefile
└── requirements.txt
```
