## Purpose

Automates the conversion of accepted Issue submissions into pull requests, streamlining the contribution workflow while maintaining validation and quality checks.

## ADDED Requirements

### Requirement: Action shall trigger on Accept label
The system SHALL trigger a GitHub Action workflow when an Issue receives the "Accept" label.

#### Scenario: Accept label added to Issue
- **WHEN** maintainer adds "Accept" label to an Issue
- **THEN** GitHub Action workflow starts automatically

#### Scenario: Other labels do not trigger Action
- **WHEN** any label other than "Accept" is added to an Issue
- **THEN** GitHub Action workflow does not start

### Requirement: Action shall validate Issue fields
The system SHALL validate all Issue fields before creating a PR:
- All required fields are present
- Field formats match schema requirements
- `id` is unique in the database
- At least one evidence entry is provided

#### Scenario: Valid Issue submission
- **WHEN** Issue contains all required fields with valid formats
- **THEN** Action proceeds to create PR

#### Scenario: Invalid Issue submission
- **WHEN** Issue contains missing or invalid fields
- **THEN** Action fails with descriptive error comment on Issue

#### Scenario: Duplicate ID
- **WHEN** Issue contains an ID that already exists in `known_ai_artists.json`
- **THEN** Action fails with error comment indicating duplicate ID

### Requirement: Action shall create branch and PR
The system SHALL create a new branch named `add-artist/<id>` and a pull request with the entry added to `known_ai_artists.json`.

#### Scenario: PR creation
- **WHEN** Issue passes validation
- **THEN** Action creates branch `add-artist/<id>` and opens PR with:
  - Entry inserted alphabetically by `id`
  - `updated` field set to current date
  - `added` and `verified` fields set to current date
  - PR description includes Issue link and entry summary

#### Scenario: PR triggers validation
- **WHEN** PR is created
- **THEN** existing `validate.yml` workflow runs automatically on the PR

### Requirement: Action shall handle evidence parsing
The system SHALL parse evidence entries from the Issue textarea format into the JSON schema format.

#### Scenario: Evidence parsing
- **WHEN** Issue contains evidence lines in format "URL | Note | Date"
- **THEN** Action converts to JSON objects with `url`, `note`, `date`, `last_checked`, and `status` fields

#### Scenario: Evidence status initialization
- **WHEN** evidence entries are parsed from Issue
- **THEN** `status` field is set to "valid" and `last_checked` is set to current date
