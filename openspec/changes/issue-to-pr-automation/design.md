## Context

The Known AI Artists Database currently accepts contributions via fork-and-PR workflow. This requires contributors to:
1. Fork the repository
2. Clone locally
3. Edit JSON manually
4. Run validation
5. Submit PR

This creates friction and limits contributions. The goal is to lower the barrier while maintaining quality through maintainer review.

## Goals / Non-Goals

**Goals:**
- Enable Issue-based contributions with structured forms
- Automate PR creation from accepted Issues
- Validate submissions before PR creation
- Maintain existing validation workflow on PRs

**Non-Goals:**
- Auto-merge PRs (maintainer review required)
- Modify existing validation workflow
- Support bulk submissions

## Decisions

### Decision: GitHub Issue Forms (YAML)
**Choice**: Use GitHub's YAML-based Issue forms instead of markdown templates
**Rationale**: Structured forms provide built-in validation, dropdowns, and required fields. Markdown templates are free-text and harder to parse.
**Alternatives considered**: Markdown templates (rejected - no structure), Custom bot (rejected - over-engineered)

### Decision: Trigger on Label Addition
**Choice**: Trigger workflow on `issues: [labeled]` with `Accept` label check
**Rationale**: Only maintainers can set labels (via repository settings), ensuring only reviewed Issues proceed. Alternative: trigger on Issue close (rejected - less explicit).
**Alternatives considered**: Issue close trigger (rejected), Issue comment trigger (rejected)

### Decision: Bash Script for Parsing
**Choice**: Use bash script with `jq` for Issue body parsing
**Rationale**: GitHub Actions runner has `jq` pre-installed. Keeps implementation simple without external dependencies.
**Alternatives considered**: Python script (rejected - requires setup), JavaScript action (rejected - more complex)

### Decision: Branch Naming Convention
**Choice**: Branch name format `add-artist/<id>`
**Rationale**: Clear intent, easy to identify, matches kebab-case ID format.
**Alternatives considered**: `feature/<id>` (rejected - too generic), `add/<id>` (rejected - less descriptive)

## Risks / Trade-offs

**Risk: Issue body parsing failures** → Mitigation: Comprehensive validation with descriptive error messages. Log raw Issue body for debugging.

**Risk: Concurrent submissions with same ID** → Mitigation: Check for existing branch before creating. Fail gracefully if branch exists.

**Risk: Malicious Issue content** → Mitigation: Only maintainers can set Accept label. Action runs in isolated environment with read-only permissions except for PR creation.

**Trade-off: Simplicity vs. Flexibility** → Bash script is simpler but less flexible than Python. Acceptable for current use case; can be upgraded later if needed.

## Implementation Plan

1. Create `.github/ISSUE_TEMPLATE/add-artist.yml`
2. Create `.github/workflows/issue-to-pr.yml`
3. Test with sample Issue
4. Document contribution process in README
