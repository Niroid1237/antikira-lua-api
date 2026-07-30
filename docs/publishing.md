# GitHub Pages

This repository now includes a `mkdocs.yml` configuration and a GitHub Actions workflow for publishing the documentation as a GitHub Pages site.

## Included Files

- `mkdocs.yml`
- `.github/workflows/docs.yml`

## Default Target

The current configuration targets:

```yaml
site_url: https://niroid1237.github.io/antikira-lua-api/
repo_url: https://github.com/Niroid1237/antikira-lua-api
```

If you publish from a different repository, update those values first.

## GitHub Setup

1. Push the repository to GitHub.
2. Open repository `Settings`.
3. Open `Pages`.
4. Set `Source` to `GitHub Actions`.
5. Push to `main` or `master`, or run the workflow manually.

## Workflow Behavior

The included workflow:

- installs `mkdocs`, `mkdocs-material`, and `pymdown-extensions`
- builds the docs with `mkdocs build --strict`
- uploads the generated `site` folder
- deploys it to GitHub Pages

## Local Preview

If you want to preview the site locally:

```bash
pip install mkdocs mkdocs-material pymdown-extensions
mkdocs serve
```

Then open the local URL printed by MkDocs.
