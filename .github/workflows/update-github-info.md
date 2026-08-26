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
model: gpt-4o-mini
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
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
5. Use the web-fetch tool to fetch `https://awesome-copilot.github.com/workflows/`.
6. Prefer recent items and useful workflow examples that help developers learn GitHub faster. Verify details against the fetched sources and include the source for every Blog, Changelog, or Awesome Copilot item. Keep all existing sources: `docs.github.com`, `github.blog`, and `github.blog/changelog`; add `https://awesome-copilot.github.com/workflows/` as an additional source when relevant.
7. Don't read all available articles / posts - 1-2 is enough. Remember, we can run into rate limitation if you read all articles/posts.

## Update

Use the edit tool to update only `site/content/github-info.md`. Preserve its existing structure and editorial angle, keep summaries short and practical, and add or refresh relevant recent GitHub Blog and Changelog entries without inventing details.

## Review

After making the update, use the `create-pull-request` safe output to open a draft pull request containing the change. Give it a concise title and explain what was refreshed and which official sources were used. The pull request is for Mona to review; do not write directly to the default branch. Do not include a `temporary_id` because this workflow does not need to reference the new pull request later. If a `temporary_id` is ever necessary, use only the canonical format `aw_` followed by 3-12 letters, numbers, or underscores, such as `aw_pr_update`.