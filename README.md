# RequestNetwork Organization-wide GitHub Configurations

This repository contains organization-wide GitHub configurations and reusable workflows for RequestNetwork.

## Reusable Workflows

### `add-to-project.yml`

Automatically adds issues and PRs to the [RequestNetwork project board](https://github.com/orgs/RequestNetwork/projects/3).

**Behavior:**
- Issues: Always added to project when opened
- PRs without linked issues: Added to project when opened
- PRs with linked issues (via `Fixes #X` or `Closes #X`): NOT added (the linked issue is tracked instead)

**Usage:** Add this caller workflow to your repo at `.github/workflows/auto-project.yml`:

```yaml
name: Auto Add to Project

on:
  issues:
    types: [opened]
  pull_request:
    types: [opened]

jobs:
  add-to-project:
    uses: RequestNetwork/.github/.github/workflows/add-to-project.yml@main
    secrets:
      PROJECT_TOKEN: ${{ secrets.PROJECT_TOKEN }}
```

**Requirements:**
- The `PROJECT_TOKEN` organization secret must be configured with a PAT that has `project` and `repo` scopes
