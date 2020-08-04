# Overleaf mirroring
![mirror-overleaf](https://github.com/denkiwakame/mirror-overleaf/workflows/mirror-overleaf/badge.svg?branch=master)

An automated overleaf repository mirroring at GitHub.

## Usage:
- Create your Overleaf project.
- `$ git clone` your overleaf project locally.
- Customize example workflow ans save as `.github/workflows/main.yaml`

### backup frequency setting

```yaml
on:
  push:
    branches:
      - master
  schedule:
    - cron: "0 0 * * *" # min(0-59) time(0-23) date(1-31) month(1-12) day(0-6)
```

### overleaf repository setting

```yaml
jobs:
  pull:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0 # checkout@v2 fetch --depth=1 by default
      - name: mirror-overleaf
        env:
          OVERLEAF_REPOSITORY: $SET_YOUR_OVERLEAF_GIT_REPOSITORY_URL
...
```

### Setup GitHub repository

- Create your mirroing repository at GitHub.
- Add secret tokens at `https://github.com/$your_account/$mirroring_repo/settings/secrets`.
  - `OVERLEAF_USERNAME` : overleaf account name like `denkivvakame@gmail.com`.
  - `OVERLEAF_PASSWORD` : https password for your overleaf repository.

### Textlint setting (optional)
- Create `package.json` for textlint rule and plugins. You can add additional plugins if you need.
- See https://github.com/textlint/textlint/wiki/Collection-of-textlint-rule

```yaml
{
  "name": "mirror-overleaf",
  "version": "0.0.0",
  "description": "",
  "dependencies": {
    "textlint": "^11.7.6",
    "textlint-plugin-latex2e": "^1.0.0",
    "textlint-rule-en-spell": "^1.0.5",
    "textlint-rule-ginger": "^2.2.1"
  },
  "devDependencies": {},
  "author": "denkiwakame <denkivvakame@gmail.com>",
  "license": "MIT"
}

```
