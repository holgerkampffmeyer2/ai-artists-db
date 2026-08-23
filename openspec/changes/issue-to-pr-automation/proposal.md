## Why

Community contributions to the Known AI Artists Database currently require forking the repo, editing JSON, and submitting a PR manually. This creates friction and limits contributions. An Issue-driven workflow with automated PR creation lowers the barrier while maintaining quality through maintainer review.

## What Changes

- Add GitHub Issue template for structured artist entry submission
- Create GitHub Action that triggers on "Accept" label to auto-generate PR
- Validate Issue fields against schema before PR creation
- Check for duplicate IDs
- Insert entries alphabetically and update metadata

## Capabilities

### New Capabilities
- `issue-template`: YAML-based Issue form for artist entry submission with required/optional fields
- `issue-to-pr`: GitHub Action workflow that parses Issue, validates, and creates PR with entry

### Modified Capabilities

## Impact

- `.github/ISSUE_TEMPLATE/add-artist.yml` (new)
- `.github/workflows/issue-to-pr.yml` (new)
- Repository Settings: Issue templates enabled
- Permissions: Action needs `issues: write`, `contents: write`, `pull-requests: write`
