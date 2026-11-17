---
name: update-github-info
description: Propose practical updates to the GitHub Info page using official GitHub Blog sources.
intent: Keep the GitHub Info page useful and current for developers with concise updates backed by official GitHub Blog sources.
on:
  schedule: daily
  workflow_dispatch:
  skip-if-match: 'is:pr is:open in:title "[github-info] "'
permissions:
  contents: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    base-branch: main
    branch-prefix: github-info/
    allowed-files:
      - site/content/github-info.md
    max: 1
    draft: false
  noop:
---

# Update Mona's GitHub Info website

Read `notes/mona-notes.md` before making changes.

Use these sources:
- `notes/mona-notes.md`
- GitHub Blog: https://github.blog/latest/
- GitHub Changelog: https://github.blog/changelog/

Update `site/content/github-info.md` with concise,
practical updates for readers and include source context when content comes
from the GitHub Blog or GitHub Changelog.

Open a pull request for Mona to review.
Use a pull request title that mentions Mona or GitHub Info.
Do not write directly to `main`;
rely on `safe-outputs` with `create-pull-request`.