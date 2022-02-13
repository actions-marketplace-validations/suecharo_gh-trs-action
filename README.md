# gh-trs-action

This action is for running continuous testing (CI/CD) using `gh-trs`.

See [GitHub - suecharo/gh-trs - Continuous testing (CI/CD)](https://github.com/suecharo/gh-trs#continuous-testing-cicd) for more details.

## inputs

- `gh-token`: GitHub Personal Access Token
- `repo`: **Optional** GitHub repository to publish to. (e.g., `owner/name`, default: your repository)
- `branch`: **Optional** GitHub branch to publish to. (default: `gh-pages`)
- `trs-endpoint`: **Optional** TRS endpoint to get the gh-trs configuration files. (default: your default trs endpoint)

## Usage

### Page build trigger

```yaml
name: page-build-ci

on:
  page_build: {}

jobs:
  test-and-publish:
    runs-on: ubuntu-latest
    if: "! contains(github.event.head_commit.message, 'in CI')"
    steps:
      - name: gh-trs-action
        uses: suecharo/gh-trs-action@v1
        with:
          gh-token: ${{ secrets.GITHUB_TOKEN }}
```

### Schedule trigger

```yaml
name: schedule-ci

on:
  schedule:
    - cron: "0 0 * * 0" // every Sunday at midnight

jobs:
  test-and-publish:
    runs-on: ubuntu-latest
    steps:
      - name: gh-trs-action
        uses: suecharo/gh-trs-action@v1
        with:
          gh-token: ${{ secrets.GITHUB_TOKEN }}
```
