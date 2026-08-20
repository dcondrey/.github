# .github

Default community health files for [@dcondrey](https://github.com/dcondrey) repositories.

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
