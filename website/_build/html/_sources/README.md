# 🔧 Uploading Markdown and Notebook files to Github Pages

[Jupyter Book](https://jupyterbook.org/) is built on **Sphinx** and **MyST Markdown**. It’s great for structured guides, teaching material, or research documentation.

## 1. Install Jupyter Book

In your repo environment:

```bash
pip install -U jupyter-book
```

## 2. Create a Book Skeleton

In your repo:

```bash
jupyter-book create mybook/
```

This creates a sample book structure like:

```
mybook/
  _config.yml
  _toc.yml
  intro.md
  markdown-notebooks.md
  notebooks.ipynb
```

* `_config.yml` → settings for your site (title, theme, etc.).
* `_toc.yml` → table of contents (controls sidebar navigation).

## 3. Add Your Files

* Copy your `.md` and `.ipynb` files into the `mybook/` folder, or into a parallel folder:

```
 mybook/
    ├── _config.yml
    ├── _toc.yml
    ├── intro.md
    ├── getting-started.ipynb
    └── advanced-topics.md
```

NB: These have to be within the `mybook/` directory: I succesfully got around this with symlinks (e.g. `../material/1-introducing-command-line.md 1-introducing-command-line.md`)

* Update `_toc.yml` to include them relative to this file, e.g.:

```yaml
format: jb-book
root: ../material/intro

chapters:
- file: ../material/getting-started
- file: ../material/advanced-topics
```

## 4. Build Locally

```bash
jupyter-book build mybook/
```

You’ll get a static site in `_build/html/`.
Open with:

```bash
open mybook/_build/html/index.html
```

## 5. Publish to GitHub Pages

In your repo root:

```bash
jupyter-book build mybook/
ghp-import -n -p -f mybook/_build/html
```

* Requires [`ghp-import`](https://github.com/c-w/ghp-import) (`pip install ghp-import`).
* This pushes your built site to the `gh-pages` branch.
* Then enable Pages in **Repo → Settings → Pages → Branch: gh-pages**.

Your book will be live at:
👉 `https://username.github.io/reponame/`
