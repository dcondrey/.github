<!-- repo-header:start -->
<h3 align="center">.github</h3>

<p align="center"><strong>Project documentation and resources for .github.</strong></p>

<p align="center">
  <a href="https://github.com/dcondrey/.github/actions/workflows/node-ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/dcondrey/.github/node-ci.yml?style=flat-square&labelColor=20232a&branch=main&label=CI" alt="CI"></a>
  <a href="https://github.com/dcondrey/.github/actions/workflows/codeql.yml"><img src="https://img.shields.io/github/actions/workflow/status/dcondrey/.github/codeql.yml?style=flat-square&labelColor=20232a&branch=main&label=CodeQL" alt="CodeQL"></a>
  <a href=".bestpractices.json"><img src="https://img.shields.io/badge/best%20practices-evidence%20reviewed-6a4c93?style=flat-square&labelColor=20232a" alt="Best Practices Evidence"></a>
  <a href="https://github.com/dcondrey/.github/blob/main/.github/CODE_OF_CONDUCT.md"><img src="https://img.shields.io/badge/code%20of%20conduct-Contributor%20Covenant%202.1-6a4c93?style=flat-square&labelColor=20232a" alt="Code of Conduct"></a>
  <a href="https://github.com/sponsors/dcondrey"><img src="https://img.shields.io/badge/GitHub%20Sponsors-Sponsor-EA4AAA?style=flat-square&labelColor=20232a" alt="GitHub Sponsors"></a>
</p>
<!-- repo-header:end -->

---

Any repo without its own copy of these files inherits them from here:

- [`CODE_OF_CONDUCT.md`](.github/CODE_OF_CONDUCT.md)
- [`CONTRIBUTING.md`](.github/CONTRIBUTING.md)
- [`SECURITY.md`](.github/SECURITY.md)
- [`SUPPORT.md`](.github/SUPPORT.md)
- [`FUNDING.yml`](.github/FUNDING.yml)
- [`PULL_REQUEST_TEMPLATE.md`](.github/PULL_REQUEST_TEMPLATE.md)
- [`ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE)

See [GitHub's docs on default community health files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file-for-your-organization) for how precedence works.

## Repo scaffold defaults

GitHub does **not** auto-inherit `.gitignore`, `.editorconfig`, `.gitattributes`, or `.github/dependabot.yml` the way it does the files above. These live at the same paths a new repo would need them, for use via [template repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) scaffolding:

- [`.gitignore`](.gitignore)
- [`.editorconfig`](.editorconfig)
- [`.gitattributes`](.gitattributes)
- [`.github/dependabot.yml`](.github/dependabot.yml) — `github-actions` enabled by default; uncomment other ecosystems as needed per repo

Once this repo is marked as a template, new repos can be created from it directly: `gh repo create my-new-repo --template dcondrey/.github --public`.

## Reusable workflows

Also not auto-inherited — reusable workflows have to be called explicitly with `uses:` from a workflow in the consuming repo. Commands are grounded in this account's actual CI (`crosstalk`, `userdirs`, `unicode-safety-check` for Rust; `misterdev` for Python; `zotero-validate` for Node), not guessed defaults, but every repo's build is still different — check the inputs match before relying on it.

- [`codeql.yml`](.github/workflows/codeql.yml) — CodeQL security scanning
- [`dependency-review.yml`](.github/workflows/dependency-review.yml) — flags vulnerable deps on PRs
- [`stale.yml`](.github/workflows/stale.yml) — closes inactive issues/PRs
- [`rust-ci.yml`](.github/workflows/rust-ci.yml) — fmt, clippy, test
- [`python-ci.yml`](.github/workflows/python-ci.yml) — uv sync, ruff, pytest
- [`node-ci.yml`](.github/workflows/node-ci.yml) — lint, format, typecheck, build, test

Example caller, in the consuming repo's `.github/workflows/ci.yml`:

```yaml
name: CI
on:
  push: { branches: [main] }
  pull_request: { branches: [main] }
jobs:
  ci:
    uses: dcondrey/.github/.github/workflows/rust-ci.yml@main
    with:
      manifest-path: rust/Cargo.toml
```
