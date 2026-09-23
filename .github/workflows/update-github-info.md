---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
tools:
  github:
    toolsets: [repos]
  web-fetch:
  edit:
network:
  allowed:
    - defaults
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: true
    reviewers: [mona]
---

Read `notes/mona-notes.md` before making any changes.

Use `web-fetch` to read both of these public sources:

- https://github.blog/latest/
- https://github.blog/changelog/

Use the GitHub repository tools to read repository guidance or reference files. Do not use the terminal, GitHub CLI, or sandboxed commands for that repository-reading step.

Use the information from the notes and the fetched sources to update `site/content/github-info.md`. Make only focused, relevant edits and preserve the existing Markdown structure. Review the resulting diff for accuracy and clarity.

When changes are needed, use the edit tool to modify the file, then use the `create-pull-request` safe output to open one draft pull request for Mona to review. Include a concise summary of the source updates and the resulting content changes in the pull request body. Do not write directly to `main`;
rely on `safe-outputs` with `create-pull-request`. If no update is warranted, do not open a pull request.
