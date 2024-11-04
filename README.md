# GitHub Action Mergify Stack rebase

This action rebase your pull request stack created by [mergify-cli](https://github.com/repos/Mergifyio/mergify-cli)

# Usage

<!-- start usage -->
```yaml
uses: Mergifyio/mergify-cli@v1
with:
  # Personal access token (PAT) used to rebase pull requests.
  #
  # We recommend using a service account with the least permissions necessary. Also
  # when generating a new PAT, select the least scopes necessary (repo: write).
  #
  # [Learn more about creating and using encrypted secrets](https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets)
  GITHUB_TOKEN: ${{ secrets.PERSONAL_ACCESS_TOKEN }}
```
<!-- end usage -->

# Scenarios

## Rebase pull request with a command

The GitHub action will be trigger when the comment `@mergify-cli stack rebase`
is posted.

```yaml
name: Mergify Stack Autorebase
on:
  issue_comment:
    types: [created, edited, deleted]

jobs:
  mergify-stack-auto-rebase:
    if: github.event.issue.pull_request && startsWith(github.event.comment.body, '@mergify-cli stack rebase')
    runs-on: ubuntu-24.04
    steps:
      - name: Run mergify stack github-action-auto-rebase
        uses: Mergifyio/mergify-cli@v1
        with:
          GITHUB_TOKEN: ${{ secrets.PERSONAL_ACCESS_TOKEN }}
```
