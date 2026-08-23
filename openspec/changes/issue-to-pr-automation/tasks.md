## 1. Issue Template Setup

- [ ] 1.1 Create `.github/ISSUE_TEMPLATE/add-artist.yml` with required fields
- [ ] 1.2 Add field validation for ID (kebab-case), type (dropdown), ai_confidence (dropdown)
- [ ] 1.3 Add evidence textarea with format description
- [ ] 1.4 Test Issue template creation in repository

## 2. GitHub Action Workflow

- [ ] 2.1 Create `.github/workflows/issue-to-pr.yml` with `issues: [labeled]` trigger
- [ ] 2.2 Add `Accept` label check in job condition
- [ ] 2.3 Implement Issue body parsing with `jq` and bash
- [ ] 2.4 Add field validation (required fields, format checks)
- [ ] 2.5 Add duplicate ID check against `known_ai_artists.json`
- [ ] 2.6 Implement branch creation (`add-artist/<id>`)
- [ ] 2.7 Implement entry insertion (alphabetical order, metadata updates)
- [ ] 2.8 Implement PR creation with description and Issue link

## 3. Permissions and Configuration

- [ ] 3.1 Configure repository permissions for GitHub Actions
- [ ] 3.2 Set up branch protection rules (if needed)
- [ ] 3.3 Test with sample Issue submission

## 4. Documentation

- [ ] 4.1 Update README.md with contribution workflow
- [ ] 4.2 Add examples of Issue submission
