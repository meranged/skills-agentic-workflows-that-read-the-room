---
name: update-github-info
description: Refresh the GitHub Info content with concise, source-backed updates for Mona's website.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine:
  id: copilot
  bare: true
  harness:
    max-retries: 0
max-turns: 20
timeout-minutes: 10
concurrency:
  group: update-github-info
  cancel-in-progress: false
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    draft: true
---

# Update GitHub Info

Update Mona's GitHub Info website with a small, useful editorial update.

## Research

1. Read `notes/mona-notes.md` with the GitHub repository API tools and follow its editorial guidance.
2. Read the current `site/content/github-info.md` with the GitHub repository API tools before editing it.
3. Use the web-fetch tool to fetch `https://github.blog/latest/`.
4. Use the web-fetch tool to fetch `https://github.blog/changelog/`.
5. Prefer recent items that help developers learn GitHub faster. Verify details against the fetched sources and include the source for every Blog or Changelog item.
6. Read external public guidance with web-fetch when it is needed to understand a GitHub feature or workflow detail.
7. Do not read every available article or post; 1-2 relevant items are enough.

## Update

Use the edit tool to update only `site/content/github-info.md`. Preserve its existing structure and editorial angle, keep summaries short and practical, and do not invent details. Use GitHub repository API tools for repository guidance and reference files; do not use terminal, CLI, or sandboxed commands to read repository files.

## Review

After making the update, use the `create-pull-request` safe output to open a draft pull request for Mona to review. Do not write directly to the default branch. Give the pull request a concise title and explain what was refreshed and which official sources were used.