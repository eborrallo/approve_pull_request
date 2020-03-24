# Auto Approve GitHub Action

**Name:** `eborrallo/approve_pull_request`

Automatically approve specific GitHub pull requests. The `GITHUB_TOKEN` secret and number of pull request must be provided as the `github-token` input for the action to work.


## Usage instructions

Create a workflow file (e.g. `.github/workflows/approve_pull_request.yml`) that contains a step that `uses: eborrallo/approve_pull_reques@1.0.0`. Here's an example workflow file:

```yaml
name: Approve
on: pull_request

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: eborrallo/approve_pull_reques@1.0.0
      with:
        github-token: "${{ secrets.GITHUB_TOKEN }}"
        number: "1"
```


Combine with an `if` clause to only auto-approve certain users. For example, to auto-approve [Dependabot][dependabot] pull requests, use:

```yaml
name: Auto approve

on:
  pull_request

jobs:
  auto-approve:
    runs-on: ubuntu-latest
    steps:
    - uses: eborrallo/approve_pull_reques@1.0.0
      if: github.actor == 'dependabot[bot]' || github.actor == 'dependabot-preview[bot]'
      with:
        github-token: "${{ secrets.GITHUB_TOKEN }}"
        number: "1"
```


[dependabot]: https://github.com/marketplace/dependabot