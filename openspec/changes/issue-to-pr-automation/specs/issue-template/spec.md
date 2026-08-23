## Purpose

Provides a structured YAML-based Issue form for community members to submit new AI artist entries with all required fields, ensuring consistent and valid submissions.

## ADDED Requirements

### Requirement: Issue template shall provide structured form
The system SHALL provide a GitHub Issue template named "Add AI Artist Entry" that presents a structured form with the following fields:
- `id`: Unique kebab-case identifier (required)
- `name`: Primary artist/project name (required)
- `aliases`: Comma-separated alternative names (optional)
- `type`: artist, project, or collective (required, dropdown)
- `labels`: Comma-separated record labels (optional)
- `ai_confidence`: high, medium, or low (required, dropdown)
- `evidence`: One evidence entry per line with URL, note, and date (required, textarea)

#### Scenario: User creates Issue with template
- **WHEN** user clicks "New Issue" and selects "Add AI Artist Entry"
- **THEN** system presents a structured form with all required and optional fields

#### Scenario: Required fields validation
- **WHEN** user submits Issue without filling required fields
- **THEN** system prevents submission and highlights missing fields

### Requirement: Issue template shall enforce field formats
The system SHALL validate the following formats at Issue creation time:
- `id`: Only lowercase letters, numbers, and hyphens (kebab-case)
- `type`: Only values "artist", "project", or "collective"
- `ai_confidence`: Only values "high", "medium", or "low"
- `evidence`: Each line must follow format "URL | Note | Date (YYYY-MM)"

#### Scenario: Invalid ID format
- **WHEN** user enters ID with uppercase letters or special characters
- **THEN** system shows validation error for ID field

#### Scenario: Invalid evidence format
- **WHEN** user enters evidence line without proper separator or date format
- **THEN** system shows validation error for evidence field

### Requirement: Issue template shall add triage label
The system SHALL automatically add the "triage" label to Issues created from this template.

#### Scenario: Issue created with template
- **WHEN** user successfully submits Issue using "Add AI Artist Entry" template
- **THEN** Issue is created with "triage" label applied
