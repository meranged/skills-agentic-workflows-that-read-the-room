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
model: gpt-4.1
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

Keep Mona's GitHub Info website current with a small, useful editorial update.

## Research

1. Read `notes/mona-notes.md` through the repository API tools and follow its editorial guidance.
2. Read the current `site/content/github-info.md` through the repository API tools before editing it.
3. Use the web-fetch tool to fetch `https://github.blog/latest/`.
4. Use the web-fetch tool to fetch `https://github.blog/changelog/`.
5. Prefer recent items that help developers learn GitHub faster. Verify details against the fetched official sources and include the source for every Blog or Changelog item.

## Update

Use the edit tool to update only `site/content/github-info.md`. Preserve its existing structure and editorial angle, keep summaries short and practical, and add or refresh relevant recent GitHub Blog and Changelog entries without inventing details.

## Review

After making the update, use the `create-pull-request` safe output to open a draft pull request containing the change. Give it a concise title and explain what was refreshed and which official sources were used. The pull request is for Mona to review; do not write directly to the default branch.

## Note
GitHub Blog, GitHub Changelog, safe-outputs, create-pull-request, and pull request