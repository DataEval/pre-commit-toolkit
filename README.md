# Pre-commit-list

We have recommended a set of static code analysis [rules](./python/pre-commit-config.yaml), primarily targeting repositories with Python code. For details on the checks performed by each rule and troubleshooting guidance, please refer to the table below.

| Rule                                 | Description                                 | Debug                                 | Notes                                 | Ignore Example                                  |
| ------------------------------------ | ------------------------------------------- | ------------------------------------- | ------------------------------------- | ----------------------------------------------- |
| [black](https://github.com/psf/black) | Python code formatter                       |                                       |                                       | single-line format:`# fmt: skip`                |
| [flake8](https://github.com/PyCQA/flake8) | Check the style and quality of some python code |                                       |                                       | single-line format:`# noqa: F401`<br>command args:`--ignore=F401` |
| [isort](https://github.com/PyCQA/isort) | Python utility / library to sort imports    |                                       | Sort rules: sort imports alphabetically and automatically separate into sections and by type | single-line format:`# isort:skip`               |
| [codespell](https://github.com/codespell-project/codespell) | Check code for common misspellings          |                                       |                                       | single-line format:`# codespell:ignore <words>`<br>command args:`--skip=doc/en/usage.md` |
| [mdformat](https://github.com/hukkin/mdformat) | CommonMark compliant Markdown formatter     |                                       |                                       |                                                 |
| [pymarkdown](https://github.com/jackdewinter/pymarkdown) | Markdown linter                             | You can use args: `[fix]` to fix errors automatically. | There will be a conflict between mdformat and pymarkdown when an empty YAML file exists.<br> | single-line format:(Must be at line start) `<!-- pyml disable-next-line -->`<br>command args:`- entry: "pymarkdown -d MD013,MD041,MD010"` |
| [mypy](https://github.com/pre-commit/mirrors-mypy) | Static type checker for Python (variables and functions) |                                       |                                       | single-line format:`# type: ignore`,<br>command args:`--disable-error-code attr-defined` is one of args |
| [pylint](https://github.com/pylint-dev/pylint) | Python code analysis tool                   |                                       |                                       | single-line format:`# pylint: disable=W0401,W0614`<br>command args:`--disable=E0402,E0401` |
| [gitleaks](https://github.com/gitleaks/gitleaks) | Detect secrets (passwords, API keys, tokens) in git repos/files |                                       | If you configure .gitleaks.toml, then the demo configuration in .pre-commit-config.yaml would be as follows:<br><pre>- repo: https://github.com/gitleaks/gitleaks<br>  rev: v8.23.1<br>  hooks:<br>  - id: gitleaks<br>    entry: "gitleaks dir"<br>    args: \[<br>      "-c=.gitleaks.toml",<br>      "--verbose",<br>      "--redact=50"<br>    \]</pre> | single-line format: `# gitleaks:allow`(Though offical example is [gitleaks](https://github.com/gitleaks/gitleaks?tab=readme-ov-file#gitleaksallow),this way can avoid of confliction with flake8)<br>configure way:Use `disabledRules = [ "generic-api-key"]` in [.gitleaks.toml](https://github.com/gitleaks/gitleaks/blob/master/.gitleaks.toml) |
| [markdown-link-check](https://github.com/tcort/markdown-link-check) |checks all of the hyperlinks in a markdown text to determine if they are alive or dead|  | Current version mistake `/A/B` format as an error. |single-line format:`single-line format:` <br> command args: `-i http://example.net` |
# Quick Start

1. Installation
 
Just run:`pip install pre-commit`, details please refer to [pre-commit](https://pre-commit.com/)

2. Configure

Copy [python/pre-commit-config.yaml](./python/pre-commit-config.yaml) to your project root.

# Citation
In our configure,we used example form [lmdeploy](https://github.com/InternLM/lmdeploy/blob/main/.github/md-link-config.json) .
