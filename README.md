# RequestNetwork Organization-wide GitHub Configurations

This repository contains organization-wide GitHub configurations and reusable workflows for RequestNetwork.

## Reusable Workflows

### `add-to-project.yml`

Automatically adds issues to the [RequestNetwork project board](https://github.com/orgs/RequestNetwork/projects/3).

**Behavior:**
- Issues: Added to project when opened
- PRs: NOT added (PRs should be linked to issues, which are tracked instead)

**Usage:** Add this caller workflow to your repo at `.github/workflows/auto-project.yml`:

```yaml
name: Auto Add to Project

on:
  issues:
    types: [opened]

jobs:
  add-to-project:
    uses: RequestNetwork/.github/.github/workflows/add-to-project.yml@main
    secrets:
      PROJECT_TOKEN: ${{ secrets.PROJECT_TOKEN }}
```

**Requirements:**
- The `PROJECT_TOKEN` organization secret must be configured with a fine-grained PAT that has:
  - Repository permissions: `Issues: Read-only`
  - Organization permissions: `Projects: Read and write`
